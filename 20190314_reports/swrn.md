Learning Implicitly Recurrent CNNs Through Parameter Sharing
===

Pedro Savarese, Michael Maire

[paper](https://arxiv.org/abs/1901.09615)

@cohama


## どんなもの?

- 畳み込み層の重みを再利用して軽量化する手法
- 重みはテンプレート k 個の線型結合として表す
- WideResNet と同等の構造でより少ないパラメータ、高い精度を実現 (NAS 系にせまる精度)

## 技術や手法の肝は？

- WideResNet のブロックごとに重みテンプレートを k 個用意 (k はハイパーパラメータ)
- 各レイヤーの重みは k 個のテンプレートの線形結合として表す (W=α T)
- 各 α は学習させる
- テンプレート自体の重みも学習させる
- 結果、パラメータ数が普通は O(L C^2 K^2) のところを O(k C^2 K^2) にできる (つまり k / L)
- パラメータをどれくらい使い回せているかを各層の α のコサイン類似度で測る
  - コサイン類似度が高くなるような正則化を入れてループ構造を作る (implicit recurrent)

## どうやって有効だと検証した？

- CIFAR-10, CIFAR-100, ImageNet でベースラインの WideResNet の他、DenseNet、ResNeXt、NAS 系とも比較
- CIFAR-10 error rate 2% 台
  - ENAS より強くて ENAS よりも少しだけ訓練時間短い
- コサイン類似度で似てるところを共通に (陽に Recuurent に) してもエラー率 0.02% 増えるだけ


## 先行研究と比べて何がすごい？

- hypernetwork という先行研究がある。ネットワーク構造をネットワーク自身で記述する
  - ただし、パラメータ削減という観点ではなかった


## 議論はある?

- k=1 でもそこそこ精度が出ている。普通のリカレントとは違う？


## 次に読むべき論文

- hypernetwork
- neural turing machine
