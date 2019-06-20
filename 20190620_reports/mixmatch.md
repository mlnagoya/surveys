MixMatch: A Holistic Approach to Semi-Supervised Learning
===

David Berthelot, Nicholas Carlini, Ian Goodfellow, Nicolas Papernot, Avital Oliver, Colin Raffel
(Google Research)

[paper](https://arxiv.org/abs/1905.02249v1)

@cohama


## どんなもの?

- MixMatch という半教師ありの手法を考案
- 250 ラベルで CIFAR-10 のエラー率 11% (他手法は38%)

## 技術や手法の肝は？

- ラベルなしデータから K 種類の Augment されたデータを作る
- 上のデータに対してモデルで推論する
- 結果を Sharpen する (温度付き softmax みたいなやつ？)
- ラベル付きデータ+教師と上で作ったラベルなしデータを混ぜる (混合データ)
- 教師ありデータと混合データを MixUp する
  - これは普通に cross entropy
- 教師なしデータと混合データを MixUp する
  - sharpen されたラベルとの二乗誤差

## どうやって有効だと検証した？

- CIFAR-10, CIFAR-100, SVHN, STL-10 で検証
- VAT, Πモデル, などと比較
  - とくにラベル数が少ない場合で他手法を大きく上回る性能
- MixMatch の個別の要素で効果を確認
  - ラベルなしデータに対する MixUp がないとエラー率 +20%


## 先行研究と比べて何がすごい？

- Entropy Minimization, Consistency Regularization, Regularization を融合した手法

## 議論はある?

- 転移学習とくらべると？


## 次に読むべき論文
- 
