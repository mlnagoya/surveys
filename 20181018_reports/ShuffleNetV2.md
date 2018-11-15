ShuffleNet V2: Practical Guidelines for Efficient CNN Architecture Design
====

Ningning Ma, Xiangyu Zhang, Hai-Tao Zheng, Jian Sun

[arXiv](https://arxiv.org/abs/1807.11164)

@cohama


## どんなもの?

- 軽量なモデルのためのガイドラインを作成。そのガイドラインの正しさを実験で確かめた
  - 畳み込み間のチャネル数を合わせた方がメモリ効率が良い
  - 過度な Group Conv はメモリ効率を悪化させる
  - ネットワークの枝分かれが多いと (GPU 内の)並列度が下がる
  - elementwise なオペレーション (ReLU とか Add とか) は FLOPs は小さくても実行時間は無視できない
- ガイドラインに従った、高速で高精度なネットワークを提案

## どうやって有効だと検証した？

- 各ガイドラインについて、実験用のネットワークを組んで実際に高速化に寄与することを実行時間 (Batches/sec) で確認
  - その際、同 FLOPs で計算時間に差があることも確認している
- ShuffleNet V2 の様々なバリエーションと既存のネットワークを比較
  - FLOPs、精度、実行時間で比較

## 技術や手法の肝は？

- 各ガイドラインに従い ShuffleNet V1 を改良
  - Channel Split (チャネルを分割し、片側は 1x1 → 3x3 1x1、もう片側はショートカット)
  - Group Conv 使わない
  - このとき bottleneck っぽくはせずに全部チャネル数同じにする
  - Concat 後の ReLU なくす


## 先行研究と比べて何がすごい？

- FLOPs じゃなくてちゃんと実行時間を測って比較している
  - モデルが軽量かどうかを FLOPs で議論することが多いが実際の計算時間とは乖離がある。実際に計算時間を測るべき
- Channel split は高速化だけじゃなくて DenseNet と同じ feature reuse ともみなせる。なので精度もいい


## 議論はある

- NASNet みたいなのは遅いけど、本論文のガイドラインも評価指標に加えるともっと早くて精度のいいネットワーク作れるかもね

## 次に読むべき論文

- ShuffleNet: An Extremely Efficient Convolutional Neural Network for Mobile Devices (https://arxiv.org/abs/1707.01083)
- MobileNets: Efficient Convolutional Neural Networks for Mobile Vision Applications (https://arxiv.org/abs/1704.04861)
