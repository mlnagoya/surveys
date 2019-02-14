Convolutional Neural Networks with Layer Reuse
===

Okan Köpüklü, Maryam Babaee, Stefan Hörmann, Gerhard Rigoll


[paper](https://arxiv.org/abs/1901.09615)

@cohama


## どんなもの?

- 畳み込み層の重みを再利用して軽量化する手法を考案した
- ShuffleNet、MobileNet と同等の精度でパラメータ数をさらに削減

## 技術や手法の肝は？

- AlexNet の学習済みのフィルタを観察すると、同じようなパターンを別々の層で学習している
  - フィルタを再利用することで冗長性を排除してより軽量なネットワークが作れるのでは
- (conv -> channel shuffle) の構成を N 回繰り返す。(conv の重みは同じ)

## どうやって有効だと検証した？

- CIFAR-10, CIFAR-100, Fashion-MNIST それぞれで最適な繰り返し回数を探索
  - 10〜14 回繰り返すのが強い
- ShuffleNet, MobileNet と精度を比較
  - 負けてるがパラメータ数は小さいと言っている
  - でもトータルの量はそんな減ってない...


## 先行研究と比べて何がすごい？

- Layer Reuse を考案した


## 議論はある?

- Layer の範囲にとどまらず、チャネル方向にも再利用するような FRU も考えられる
- 所感
  - 同精度くらいのネットワークで比較しているけど実は高い精度だせないのでは...?


## 次に読むべき論文

- https://arxiv.org/abs/1807.11164
  - ShuffleNet V2
