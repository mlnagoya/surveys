cuDNN: Efficient Primitives for Deep Learning
====

Sharan Chetlur, Cliff Woolley, Philippe Vandermersch, Jonathan Cohen, John Tran, Bryan Catanzaro, Evan Shelhamer

[arXiv](https://arxiv.org/abs/1410.0759)

@cohama


## どんなもの?

- Deep Learning 用の数値計算ライブラリ cuDNN を作った
- Caffe 上の実装で 36 % 高速化

## 技術や手法の肝は？

- lowering (im2col) による Convolution の実装を作った
- 行列演算をサブマトリックスに分解→それごとに GPU のオンチップメモリに読み込み→計算
- 愚直に lowering するとメモリ使用量が多くなるが、lowering された行列はオンチップメモリ上でしか持たないようにした

## どうやって有効だと検証した？

- Caffe、cuda-convnet2 という既存実装と比較
- minibatch size 100 までの畳込み演算は既存より速い
  - 100超えると cuda-convnet2 が速い

## 先行研究と比べて何がすごい？

- 愚直な lowering だとメモリ使用量が多すぎる
- FFT を使う方法もあるが、一時メモリ使用量のが多いのと stride 1 以外のときにあまりパフォーマンスがよくない
- Convolution 専用のアルゴリズムを考える方法と比較すると
  - 畳込みには11次元のパラメータがあるがそれ上のコーナーケースを洗い出すのが大変
  - 例えば既存実装の cuda-convnet2 は minibatch 64 までならそこそこ速いがそれ以下だと非常に遅い

## 次に読むべき論文

- [Fast Algorithms for Convolutional Neural Networks](http://openaccess.thecvf.com/content_cvpr_2016/papers/Lavin_Fast_Algorithms_for_CVPR_2016_paper.pdf)
