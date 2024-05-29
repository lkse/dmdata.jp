---
title: 緊急地震速報を適切に利用するために必要な受信端末の機能および配信能力に関するガイドラインの表示
---

## 緊急地震速報ガイドラインの表示（端末用）

EEW Client by DMDATA.JP のソフトウエアを対象としています。

[緊急地震速報を適切に利用するために必要な受信端末の機能及び配信能力に関するガイドライン(気象庁HP)](https://www.data.jma.go.jp/eew/data/nc/katsuyou/guideline/guideline.pdf)

---

**気象庁が緊急地震速報(予報)・リアルタイム震度電文を発表してから緊急地震速報(予報／業)等を端末に届けるのに要する時間**

気象庁が緊急地震速報を発表してからDMDATA.JPのWebSocketによる配信、ソフトウエアで表示するまでの時間は1秒未満でありますが、
インターネット経由での配信であるため、通信状況によっては利用者に到達するまで1秒以上かかる場合があります。

---

**気象庁から端末まで、配信を途切れさせないような対策**

WebSocketによる常時接続を行い、Pingチェックを一定間隔に行っています。
切断が確認されると、ランダムな待機時間（5～30秒程度）を経た後、再接続を行います。

---

**時間合わせ**

ソフトウエア上で、時間合わせを行い1秒未満の誤差を維持します。

---

**配信・許可事業者によるサポート/配信・許可事業者への連絡**

メールや、[お問い合わせページ](/contact)にて対応します。

---

**耐震固定等地震の揺れへの対策**

気象庁からの受信・ソフトウエアへの配信はクラウド上で行っており対策済みとします。

---

**無停電化**

気象庁からの受信・ソフトウエアへの配信はクラウド上で行っており対策済みとします。

---

**端末の冗長化**

利用者側で行うか選択します。

---

**常時接続できる回線**

WebSocketによる接続を行い、常時接続を取ります。

---

**専用線等信頼性の高い回線**

インターネットによる配信のため、利用できません。

---

**サーバー端末間の物理回線の冗長化**

インターネットによる配信のため、利用できません。

---

**予想した猶予時間**

猶予時間等関係なく、ソフトウエアでユーザーが設定した表示する条件に合致した場合はすべて表示（報知）を行います。
また、表示については最終報受信後300秒または、主要動到達後30秒（到達予想がない場合は、この条件は無し）のいずれも到達した場合か、主要動到達後、新しい別の地震による緊急地震速報を予想した場合は古い地震による緊急地震速報の表示を終了します。


---

**予想した震度、長周期地震動階級等や構造物の詳細な揺れの大きさ**

ソフトウエアでユーザーが設定した表示する条件に合致した場合は予想震度、長周期地震動階級・絶対速度応答スペクトル、主要動到達までの秒数を表示します。

---

**精度情報**

1点観測点に基づく緊急地震速報、100gal越え緊急地震速報、1点によるPLUM法のみの緊急地震速報（以下、精度の低い緊急地震速報という）は表示しません。
ただし、ユーザーが設定した場合は精度の低い緊急地震速報を用いた予想が利用ができます。

---

**深発地震についての緊急地震速報**

震源由来震度（従来法）、長周期地震動階級・絶対速度応答スペクトルの予想について、深さ150kmよりも深い地震については行いません。
なお、波面伝播非減衰震度（PLUM法）については、観測したデータが存在する場合は予想を行います。

---

**放送・報知内容**

予想震度、主要動到達までの秒数を表示し、表示開始時に、チャイム等を再生しお知らせします。
震度については読み上げを行い（予想した震度階級が上昇した場合は再度読み上げ、下がる場合は読み上げない）、主要動到達までの秒数を読み上げます（設定で無効化ができます）。

主要動到達までの予想については、PLUM法による震度を用いる場合は行いません。

---

**緊急地震速報で制御、放送、報知を行った後に同一地震または別の地震について提供される緊急地震速報**

同一の地震、別の地震（情報を統合して表示）で予想震度が上昇した場合は、再度読み上げてお知らせするなどします。

複数の地震による主要動到達までの予想は、PLUM法による震度を用いていない場合は、早い順に表示・読み上げ等を行い、主要動到達後再度、別の地震による主要動到達までの表示・読み上げを行います。
PLUM法による震度を用いている場合は、主要動到達までの予想は行いません。

---

**キャンセル報**

キャンセル法を受信した場合は、その旨を表示し予想の表示を終了します。

---

**試験・訓練**

このソフトウエアでは利用しません。