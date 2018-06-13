A novel channel pruning method for deep neural network compression
===

Yiming Hu, Siyang Sun, Jianquan Li, Xingang Wang, Qingyi Gu

[arXiv](https://arxiv.org/abs/1805.11394)

2018/5/29 @cohama


## どんなもの？

- CNN の Convolution のチャネルを削減する Channel Pruning により高速化 (FLOPs: 1/3) と省メモリ化 (Params: 1/8) しつつ SOTA に匹敵する精度を維持
- どの Channel を選択するかの決定に遺伝的アルゴリズムを応用した手法を適用


## どうやって有効だと検証した？

- ImageNet, CIFAR-10, CIFAR-100, SVHN に対して、削減前のものと精度を比較
- ThiNet, Taylor という他のパラメータ削減手法とも比較


## 技術や手法の肝は？

- あるレイヤーのあるチャネルを削減するかどうかをベルヌーイ分布のサンプリングで決める
- 0/1にエンコードされた情報を染色体として遺伝的アルゴリズムを適用
- 各レイヤーで削減前と削減後の活性前の出力の二乗誤差を Layer-wise Loss として定義し、これを最小化させるようにする
- レイヤー毎に進化のイテレーションを回す
- 最初のレイヤーを回す→Fine Tune→次のレイヤー→Fine Tune
- Fine Tune は蒸留で行う


## 議論はある？

(paper 自体にはないけど)

- 感想
  - Pruining rate 決めるの大変そう


## 先行研究と比べて何がすごい？

- 重みだけの二値化
  - 省メモリできる
  - 高速化のためには専用ハードいる
- 全部二値化
  - 精度が unacceptable
- スパース化
  - 実行時のメモリ使用量を減らせない
  - 高速化のためには専用ハードかソフトの対応 (cuDNN とかのことか?) が必要
- 低ランク近似
  - FC にはいいけど畳み込みは微妙
- ThiNet
  - 貪欲法を使ってるが、組み合わせ最適化問題には適切でない
  - Pruning が遅い


## 次に読むべき論文は？

- [ThiNet: A Filter Level Pruning Method for Deep Neural Network Compression](https://arxiv.org/abs/1707.06342)
- [Learning to Prune Filters in Convolutional Neural Networks](https://arxiv.org/abs/1801.07365)
