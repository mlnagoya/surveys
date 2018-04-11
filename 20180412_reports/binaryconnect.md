論文のタイトルを書く
===

2015/11/02

BinaryConnect: Training Deep Neural Networks with binary weights during propagations

Courbariaux, Matthieu, Bengio, Yoshua, and David, Jean-Pierre.

[arXiv](https://arxiv.org/abs/1511.00363)

@cohama


## どんなもの？

- 二値化 (-1 と +1) した重みで学習を行う BinaryConnect という手法を考案した
- BinaryConnect は正則化の効果がある
- MNIST、CIFAR-10、SVHN のデータセットでほぼ SOTA 相当の精度
- 計算量は約 1/3、メモリ使用量は 1/16 という見積もり
  - (FPGA のような)専用ハードウェアを使えば早くなるよ


## どうやって有効だと検証した？

- 正則化の効果を Permutation-invariant MNIST、CIFAR-10、SVHN でそれぞれ実験し、他の手法 (No-reguralizer、Dropout、DropConnect) と精度や学習曲線を比較


## 技術や手法の肝は？

- 実数値を取る重み自体は記憶しつつ、Forward と Backward 時に重みを二値化して計算
- 重みの更新時は実察の重みに対して行う
- 二値化の方法として決定的なものと確率的の2種類ある
  - 決定的
    - 実際の重みの sign をとるだけ
    - 訓練した重みは推論時にも用いる
  - 確率的
    - 実際の重みの大きさに応じて確率的に +1 または -1 をとるようにする
    - 訓練時だけ二値化。推論時は実際の重みの方を用いる
    - 正則化の効果を狙うため?
- 実際の重みのクロッピングも行う ([-1, 1] の範囲)


## 議論はある？

(paper 自体にはないけど)

- 感想
  - 確率的な方は推論時に実際の重みに戻しちゃうのはなんで
  - で実際どれくらい早くなったの?


## 先行研究と比べて何がすごい？

- Backpropagation ではなく Expectation Backpropagation という手法を使って二値化する先行研究あり。
  - 重みだけでなく入出力も二値化
  - 全結合ではいい精度だけど畳み込みに難あり
- ternary (三値化; -1, 0, +1)
  - 普通に学習したあとで最終的な重みを三値化
  - 三値化したあとで再学習
    - 三値化した重みで計算したロスで実際の重みを学習
  - 提案手法は常に二値化しているので計算量的に有利


## 次に読むべき論文は？

- [XNOR-Net: ImageNet Classification Using Binary Convolutional Neural Networks](https://arxiv.org/abs/1603.05279)
  - 重みだけでなく入出力も二値化する XNOR-Net の提案
