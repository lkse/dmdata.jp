---
slug: /reference/conversion/json/
title: JSON化データについて
---

## 概要

Project DM-D.S.Sでは[気象庁防災情報XMLフォーマット](http://xml.kishou.go.jp/)について、取り扱いの容易化を目的としたJSON化を行っています。

XMLデータをJSON化するデータは利用頻度の高いデータとし、独自のスキーマ定義に沿った変換を行うもとしています。

## 変換に伴うリスク

XMLデータをJSON化する際、変換する時間が最大1秒程度（基となるXMLデータの配信遅延はありません）かかります。
また、変換に失敗する恐れや、想定していないデータの配信が発生することがあります。


## APIの取り扱い

[Telegram List v2](/reference/api/v2/telegram.list) と [WebSocket v2](/reference/api/v2/websocket)でJSON化データを取得することができます。

JSON化データを取得する方法はAPIのリファレンスを参照してください。

## JSON スキーマ

JSONスキーマの型定義については、[API v2 #型表現](/reference/api/v2/#型表現)を参照ください。

| 配信区分       | スキーマ名                   | 対象とする<br/>データ種類コード | バージョン | 
| -------------- | ---------------------------- | ------------------------------ | ---------- | 
| 地震・津波関連 | [earthquake-information](schema/earthquake-information)              | VXSE51, VXSE52, VXSE53         | 1.0.0      | 
| 地震・津波関連 | [earthquake-explanation](schema/earthquake-explanation)              | VXSE56                         | 1.0.0      | 
| 地震・津波関連 | [earthquake-counts](schema/earthquake-counts)                        | VXSE60                         | 1.0.0      | 
| 地震・津波関連 | [earthquake-hypocenter-update](schema/earthquake-hypocenter-update)  | VXSE61                         | 1.0.0      | 
| 地震・津波関連 | [earthquake-nankai](schema/earthquake-nankai)                        | VYSE50, VYSE51, VYSE52         | 1.0.0      | 
| 地震・津波関連 | [tsunami-information](schema/tsunami-information)                    | VTSE41, VTSE51, VTSE52         | 1.0.0      | 
| 火山関連      | [volcano-information](schema/volcano-information)                    | VFVOii (ii = 50-56), VFSVii (ii = 50-61) | 1.0.0      | 

### 共通ヘディング

```json
{
  "_originalId": "...",
  "_schema": {
    "type": "earthquake-information",
    "version": "1.0.0"
  },
  "type": "震源・震度に関する情報",
  "title": "震源・震度情報",
  "status": "通常",
  "infoType": "発表",
  "editorialOffice": "気象庁本庁",
  "publishingOffice": [
    "気象庁"
  ],
  "pressDateTime": "2021-08-12T06:05:36Z",
  "reportDateTime": "2021-08-12T15:05:00+09:00",
  "targetDateTime": "2021-08-12T15:05:00+09:00",
  "eventId": "20210812150301",
  "serialNo": "1",
  "infoKind": "地震情報",
  "infoKindVersion": "1.0_1",
  "headline": "１２日１５時０２分ころ、地震がありました。",
  "body": {}
}
```


| 階層 | フィールド | 出現条件 | 説明 |
| -- | -- | -- | -- |
| 1. | _originalId | | **String**<br/> 基となったXMLデータの電文ID |
| 2. | _schema |  | **Object**<br/> JSONスキーマ情報 |
| 2._1. | _schema.type |  | **String**<br/> JSONスキーマ名 |
| 2._2. | _schema.version |  | **String**<br/> JSONスキーマバージョン |
| 3. | type | | **String**<br/> 情報名称(Control/Title部) |
| 4. | title | | **String**<br/> 情報の標題(Head/Title部) |
| 5. | status | | **String**<br/> 情報の運用状態、取りうる値は`通常`、`訓練`、`試験`<br/> `通常`以外の情報につては内部利用にとどめること |
| 6. | infoType | | **String**<br/> 情報の発表状態、取りうる値は`発表`、`訂正`、`遅延`、`取消` |
| 7. | editorialOffice | | **String**<br/> 情報の編集官署名 |
| 8. | publishingOffice | | **Array<String\>**<br/> 情報の発表官署名又は組織名、複数入る場合がある |
| 9. | pressDateTime | | **ISO8601Time**<br/> 情報作成時刻 |
| 10. | reportDateTime | | **ISO8601Time**<br/> 情報の発表時刻 |
| 11. | targetDateTime |  | **ISO8601Time\|Null**<br/> 情報の基となった時刻、無い場合は**Null**とする |
| 12.? | targetDateTimeDubious | 情報による | **String**<br/> 情報の基となった時刻のあいまいさ |
| 13.? | targetDuration | 情報による | **String**<br/> 情報の予報期間 |
| 14.? | validDateTime | 情報による | **ISO8601Time**<br/> 情報の失効時刻 |
| 15. | eventId |  | **String\|Null**<br/> 現象ごとに割り振られたイベントID、無い場合は**Null**とする |
| 16. | serialNo |  | **String\|Null**<br/> 現象ごとに割り振られたイベントIDの発表番号、無い場合は**Null**とする |
| 17. | infoKind |  | **String**<br/> XMLデータのスキーマ名 |
| 18. | infoKindVersion |  | **String**<br/> XMLデータのスキーマバージョン |
| 19. | headline |  | **String\|Null**<br/> 情報の見出し、無い場合は**Null**とする |