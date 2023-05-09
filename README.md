# 幻闘戦　ポイント計算

# DEMO

![image](https://user-images.githubusercontent.com/48175908/236965057-5788c269-fbd5-4cc9-ae61-8c71cb820dce.png)
目標の総合等級までの必要周回数などを一覧にして表示します。

画像の場合は、画像上部の状況で以下の周回を行うことで総合等級Sに到達できることが分かります。
- クエストA：16回
- クエストB：16回
- クエストC：17回
- クエストD：17回

# Usage

## 基本情報入力

### 挑戦回数設定

「日付を選択する」または「手動で入力する」から、あと何回ポイントを獲得できるかを入力します。  

「日付を選択する」の「起点日」には、デフォルトで本日の日付が入力されています。  

「日付を選択する」の「終了日」には、デフォルトで次の木曜日の日付が入力されています。  

「日付を選択する」の「起点日の回数を含める」については、計算起点日のポイント獲得の有無に応じて設定してください。

「手動で入力する」の場合は、残りのポイント獲得回数を自身で入力してください。

### カジュアルモード

「カジュアルモードにする」にチェックを入れるとカジュアルモードとして計算を行います。  
<sub>※カジュアルモードでは、総合等級Aが上限となり、獲得ポイントが3倍となります。</sub>

## クエスト設定

各クエストABCDは、それぞれ解放順に対応しています。  順番通りに入力することを推奨します。
最後に解放されるクエストをクエストAに設定した場合、実現可能な結果が出力されない場合があります。

![image](https://user-images.githubusercontent.com/48175908/236971651-3168ca26-c4df-43d4-a8e8-1364a2386154.png)


各クエストには以下の情報を設定することができます。
- 【任意】クエスト名
- 刻印レベル
- 【任意】現在のポイント
- 平均解答時間
- クリアターン
- クイズ正解率

クエスト名は自身で分かりやすいものを任意で設定してください（最大15文字）。  
なお、計算結果には影響しないため設定しなくても問題ありません。

刻印レベルは自身がクリアするレベルを設定してください。  
刻印レベルの欄には0～34までの整数を入力することができます。

現在のポイントは、途中経過から計算を行いたい時などに使用します。  
現在のポイントに入力された値は、必要総合等級にかかわらず既に取得したものとして計算されます。  
またこの欄を使う際は、挑戦回数も入力しておくことを推奨します。

平均解答時間・クリアターン・クイズ正解率はC～SSまでのランクを選択してください。
入力された刻印レベル及びボーナスのランクから獲得できるポイントがクエスト設定欄内に表示されます。

期間内に目標の総合等級を達成するために必要な刻印レベルを調べたい際は、調べたいクエストの刻印レベルを自由に設定し、総合等級の欄が達成可能か否かで調べることが可能です。

<sub>※獲得ポイントなどは調整により変更となる場合があります。</sub>

## アルゴリズム

### 必要挑戦回数の算出

挑戦回数の算出は総当たりで行い、得られた結果の中から条件に合う最も良い結果を1つ出力します。  
必要挑戦回数については、残り挑戦回数を超過しない条件に加えて、クエスト解放日程の兼ね合いよりクエストごとに上限が設けており、その上限を超過しないものを出力します。

- クエストA：上限100回
- クエストB：上限85回（最初の15回は挑戦不可）
- クエストC：上限65回（最初の35回は挑戦不可）
- クエストD：上限50回（最初の50回は挑戦不可）

そのため、例えばクエストDの挑戦回数が36回の場合は50回中36回、さらにクエストCの挑戦回数が24回の場合は、65回中(36+24)回周回が必要となります。

なお、総挑戦回数が95/100と表示されている場合に、次のクエスト解放までに解放済みクエストが終了し新たに挑戦できない日があった場合も挑戦しなかった日としてカウントします。  
<sub>※算出に用いるデータは各種調整等により変更となる場合があります。</sub>

### 結果表示の優先度

得られた計算結果のうち、いくつかの条件でフィルターを行い、その中の1つを出力します。

1. 実現可能な組み合わせのうち、総挑戦回数が最も少ないもの。
2. 1で得られた結果のうち、各クエストの挑戦日数の合計が最も少ないもの。
3. 2で得られた結果のうち、各クエストの挑戦回数の偏りが最も小さいもの。

1について、組み合わせには何パターン化存在することが想定されますが、その中から総挑戦回数が最も少ないものをピックします。

2について、その中から各クエストの挑戦日数の合計が最も少ないものをピックします。  
例えば、同じ合計30回でも、5-5-10-10と6-6-8-10では後者の方が日を跨ぐものが多くスキップを行えない回数が多くなってしまうため、表示優先度を下げます。  

3について、1つのクエストに偏っているものの優先度を下げ、全クエストを平均的に周回するものをピックします。


## 画像化

出力された結果を1枚の画像として出力します。  
生成が失敗した場合はモーダルウィンドウを閉じて再生成してください。

# Cation

機能改修等により、記載された内容と変更になる場合があります。

本ツールは予告なく更新や公開を停止する場合があります。

サイトは端末やアプリのダークモード設定に対応しています。好みに応じてご使用ください。

# Author

* kmlnwiz
