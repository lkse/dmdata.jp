---
title:  EEWについて
---

DMDATA.JPでは今後、緊急地震速報の配信を予定しております。

その計画と、実施日時についてお知らせいたします。

## 配信の内容

気象庁から配信される緊急地震速報（予報及び警報）をそのままDMDATA.JPで再配信するものとなります。

予定している電文と配信区分は次の通りです。

* eew.forecast (緊急地震（予報）区分)
  * VXSE42 緊急地震速報（テスト）
  * VXSE44 緊急地震速報（予報）
  * VXSE45 緊急地震速報（地震動予報）（新形式） ※気象庁より提供され次第配信
* eew.warning (緊急地震（警報）区分)
  * VXSE43 緊急地震速報（警報）

各配信区分の利用料金は以下の通りです。 ※価格は税込み

* eew.forecast (緊急地震（予報）区分)
  * 月最大：1650円
  * 日割り：75円
* eew.warning (緊急地震（警報）区分)
  * 月最大：440円
  * 日割り：22円

### 配信の方法

**WebSocketによる配信のみ**の提供となります。

緊急地震速報は速報性が重視されるため、WebSocketによる即時配信が必要となるための措置です。

また、緊急地震速報の電文を事後的に参照するためのAPIを実装予定です(緊急地震（予報）区分契約者のみ)。

### JSON化データ

気象庁から送られてくるXMLデータのほか、DMDATA.JPで独自で定めたJSON化データも配信します。

## 配信を開始する時期

2022年02月の中旬から下旬に配信開始を計画しています。

現在、回線等の契約のための交渉をお願いしています。

今しばらくお待ちくださいませ。

## 利用する上での注意点

特にDMDATA.JPで緊急地震速報を利用する際の注意点と、緊急地震速報自体の特性による注意点がありますので、開発の際は下記にご留意ください。

### 開発者の方向け

* 配信データは、**必ずしも発表された順番どおりには配信されません**。
  * 0.1秒単位で発表され、処理などの差により入れ違えが発生する可能性があります。
  * 必ず、古いデータ(Serialで番号が古いなど)は破棄するか反映をしない処理を加えてください。
  * Serialは、取消時（キャンセル報）には1つ前のデータと同じSerialが振られたデータが配信されます。


* 緊急地震速報は**1秒間に最大20報程度配信**されることがあります。
  * 緊急地震速報の発表処理に係る気象庁システム上の限界となります。


* 緊急地震速報の**訓練報を配信することがあります**ので、取り扱いは十分に注意の上ご利用ください。
  * DMDATA.JPでは、訓練報など通常ではないデータは、明示的に指定しない限り配信しません。
  * アプリケーション等で訓練を表示する際、ユーザーが即座に訓練と分かる表示をしてください。


* **仮定震源**の緊急地震速報では、**震源要素をユーザーへ表示しないよう対策をするか注意文を記載**してください。
  * 仮定震源は、地震学的に意味のない仮定の値となり混乱のもととなるため表示は推奨しません。


* 緊急地震速報（警報）を使用する場合は、規模や深さを表示しないようにしてください。
* 緊急地震速報電文のリアルタイムに行なわれる（当配信サービスから見ての）**二次配信はエンドユーザーまでの到達が遅くなる可能性があるため推奨しません**。
* DMDATA.JPのデータを使い、地震動予報業務を行うことはできません。
* アプリケーション等で外部へ配布する際は、一般の方向けへの注意文を必ず明記してください。

### 一般の方向け

* 地震発生後、数秒で情報を作成するため、誤報が発生することがあります。
* 地震検知直後の情報は震源やマグニチュードの推定や、予測震度の精度が低いことがあります。
* 通常でも推定震度は1階級程度の誤差があります。
* PLUM法のみの情報・100gal検知・リアルタイム震度4.5以上検知（※仮定震源）の場合、震源要素（規模、深さ、震央）は地震学的に意味がない値となります。
* 深さ150kmより深い地震の場合、予想最大震度は発表されません（※PLUM法により発表される場合があります）。
* ご利用の通信環境により、発表から情報到達まで1秒以上かかる可能性があります。5Mbps以上の安定した通信環境をご用意ください。