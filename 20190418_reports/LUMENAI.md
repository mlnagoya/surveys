#Time series aggregation
Comparison of two global averaging approaches

##２つの時系列データの類似性を測定する
===

Submitted on 2018/02
by LumenAI（France）


http://www.lumenai.fr/blog/time-series-aggregation


---

## 個人の動機

* 2月の勉強会で、時系列データの転移学習についての論文を紹介した。UCRデータセット/時系列×85　を利用して、85×84の組み合わせで、DBA (DTW Baricenter Avaraging）によりデータセットの類似性と転移学習した場合の精度を測定すると、類似性が高いほど精度も高いことが分かったというも論文。
　https://arxiv.org/pdf/1811.01533.pdf

* 時系列の類似性を測定する方法が他にもないか、調べるとSoft-DTW、soft-DBA  というツールが紹介されている。これはDTW、DBAをsoft曲線にして微分で計算できるようにしたという論文。　　　　　　　　　　　　　　　　　
　https://arxiv.org/pdf/1703.01541.pdf　　　‥‥論文　　　　　
　https://vimeo.com/238243365　　　　　…発表動画

* 上記２つ DTW Baricenter Avaraging  vs  Soft-DTW,soft-DBA  を解説しつつ比較している資料はないか探すと、上記ブログが見つかった。

* いずれもIoTでデータ集めする企業が多く増えていて、これからはAIと口にする一方で、何をしたらいいか分からない企業が非常に多いと感じている。転移学習＋類似性の切り口で支援できるか検討するため。

## What are time series ?
### 時系列とは何ぞや？　
* ・・・省略します

## Similarity measure between pairwise of TS
### ２つの時系列データセットの類似性を測定時、　
* ユークリッド距離・・・時間のずれに対して、硬直的で使えない　　　　　　
* DTW や Soft-DTWは時間のずれを吸収し、柔軟性が高い。Soft-DTWはへ平滑化パラメータの設定によって柔軟性が変わる。

## When data reduction is needed
### 時系列データのサマライズ方法（クラスタリングや分類の際）
* クラスタリングのため…KMeans や階層的クラスタリングアルゴリズムを使ってデータをサマライズ
* 分類のため…データを部分に分けてKNN など。
* わかりやすく視覚化のため
* DTW, soft-DTW のどちらか、最終的な目的によって使い分ければよい

## Averaging several time series
### データセットの平均化：2つのツールを比較
* DBA　　: データセットの平均（重心）と、追加のデータセットとの間のDTWの二乗の合計が最小になるようにして「平均」を計算、この作業を繰り返す。

* Soft-DBA　:　データセットの平均（重心）と、追加のデータセットの間のsoft-DTW の距離の重みを最小になるようにして「平均」を計算する。平滑化パラメータの値がないと（＝DBA）曲線は固く、値が高いとなめらかに。


##Practical comparisons

DBA　vs soft-DBA(prm=1）vs soft-DBA(prm=10)


### Goal 1: クラスタリングでの比較　
### ＿＿＿＿＿UCRの１データセット　　　　
* DBA　　: ARI(グループ内の一致度)は最も高い、変動も少ない
* Soft-DBA(prm=1）　:　平滑化パラメータ＝１でARIは低下
* Soft-DBA(prm=10）:　平滑化パラメータが高いほどARIは低く、変動率も高くなる

### Goal ２: 分類での比較　その１
### ＿＿＿＿＿UCRの１データセット
* DBA　　: Classification精度=0.97
* Soft-DBA(prm=1）　:　0.74
* Soft-DBA(prm=10）:　0.72


### Goal ３: 分類での比較　その２
### ＿＿＿＿＿UCRの上記以外12データセット
* 半分はDBAが、もう半分はSoft-DBAのの精度が高い、どちらという判断は難しい
*　私にはDBAが無難に見える。


---

## ところでDBAのの基礎を作ったのは誰？


http://human.ait.kyushu-u.ac.jp/late_prof_sakoe/index.html