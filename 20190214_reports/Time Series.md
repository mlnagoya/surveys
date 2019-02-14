#Transfer learning for time series classification

##(櫻井メモ)時系列データに転移学習は有効か？

===

Submitted on 2018/11
by IRIMAS, Universit´e de Haute-Alsace, Mulhouse, France

論文リンク

https://arxiv.org/pdf/1811.01533.pdf

---
## 個人的な動機

 IoTの利用が中小企業でも増えてきて、時系列データの活用について議論が活発になっている。しかしデータ量は決して多くない。そこで転移学習の可能性を考えたい。


## 本論の著者の動機

* 時系列データへの転移学習はほとんど議論されていない。
* 深層学習が時系列でも利用るyできることが最近証明された。
* それなら転移学習も可能ではないか？


###  　
---
## どうやって検証した？

 
* モデル

時系列データを入力　=>　畳み込み層×３=>　GAP（各時系列を平均化）=>　全結合層（softmax）

* 転移学習の方法　

ソースとターゲットでで同じモデル。最後の層のみのFine-tiningは収束せず。全層でTuning

* データセット/ソースとターゲットの組み合わせ方法　
 
UCRデータセット/時系列×85　を利用。85×84通りの組み合わせで、データ類似性と転移学習の精度に相関関係があるか調査する。



## 調査結果

85のデータセットについて、転移学習なしと転移学習あり(×84通り)で比較。
DTW/動的時間収縮法、およびDTW Barycenter Averaging (DBA) の手法を用いて、時系列データの平均を求めるなどして、85×84通りの組み合わせ全てについて類似性を調査。
GPUを60台使った。

* 調査結果:Fig4

85×84通りの組み合わせ全てについて転移学習の結果をマトリックス化。縦にsource.横列にtarget
sourceで事前に学習した後、targetでfine tuningして、精度向上すれば青、劣化すれば赤、白は変化なし
全体に白が多く学習済みモデルをfinetuning後の精度劣化は殆ど起こっていない

* 調査結果:Fig5

転移学習なしのケースに対して、、青＝最も高精度のケース、赤＝最も低い精度のケースをプロットしたもの。
ソースによって精度が大きく変わることがわかる。ソースの選び方が重要。

* 調査結果:Fig6

最も近似なデータセットをソースとした場合の精度をプロットしたもの。85のうち71で、類似性の高いソースが精度向上につながっているにつながっている。


* 調査:Fig7,8,9

データ数の最も少ないデータセット３つについて、類似性の高さと転移学習結果の精度を調査。
いずれも類似性の高いソース３つについてターゲットの精度が高い。
---

## 結論

* ソースの選び方で時系列データに転移学習は有効。ソース選択にはDTW Barycenter Averaging (DBA) が使えることがわかった。

---

## アプローチが似ている日本の論文

Local Shapeletを用いた時系列分類に最適な距離尺度の選択　（神戸大学　辻本貴昭/2012）

* 時系列分類でそのデータに適する距離尺度のでがある。類似しているデータ

https://www.google.co.jp/url?sa=t&rct=j&q=&esrc=s&source=web&cd=6&ved=2ahUKEwicnYbto7LgAhWr-GEKHbeEApoQFjAFegQIBRAC&url=https%3A%2F%2Fipsj.ixsq.nii.ac.jp%2Fej%2Findex.php%3Faction%3Dpages_view_main%26active_action%3Drepository_action_common_download%26item_id%3D87179%26item_no%3D1%26attribute_id%3D1%26file_no%3D1%26page_id%3D13%26block_id%3D8&usg=AOvVaw3xtEL4TqDmzGw575v0Lkfx

## 次に読むべき論文は？

引き続き、同様の論文を探して回ります。

