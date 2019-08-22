Tracking Emerges by Colorizing Videos
===

Carl Vondrick, Abhinav Shrivastava, Alireza Fathi, Sergio Guadarrama, Kevin Murphy
(Google Research)

[paper](https://arxiv.org/abs/1806.09594)

@cohama


## どんなもの?

- 教師なしのビデオトラッキング
- 入力の最初のフレームにセグメンテーション教師を与えると、残りのフレームのセグメンテーションを自動でトラッキングして予測

## 技術や手法の肝は？

- 参照画像と対象画像の2つを用意する
- グレースケールに変換してから特徴ベクトルを出す
- 特徴ベクトル同士の対応を取る
- ピクセルの対応と参照画像の色情報をもとに、対象画像の色付けを行う
- 色があってるかどうかを損失関数にする


## どうやって有効だと検証した？

- DAVID17 Video Segmentation の平均オーバーラップで Optical Flow ベースの手法よりもすごい
- Key Point Tracking でも確かめた


## 先行研究と比べて何がすごい？

- Self supervised で強い

## 議論はある?

- 

## 次に読むべき論文
- Self-supervised Learning for Video Correspondence Flow https://arxiv.org/abs/1905.00875v5
  - この手法の改良版
