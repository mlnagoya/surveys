ShuffleNASNets: Efficient CNN models through modified Efficient Neural Architecture Search
====

Kevin Alexander Laube, Andreas Zell

[paper](https://arxiv.org/abs/1812.02975)

@cohama


## どんなもの?

- ShuffleNet V2 の論文で効率的な CNN 構築のガイドラインが示された
- そのガイドラインに従うような制約の上でのネットワークアーキテクチャ探索を行い、効率的で精度の良いネットワークを作った

## 技術や手法の肝は？

- ShuffleNet V2 で示されたガイドラインに従った上で ENAS と同等の手法でネットワークを探索
  - チャネル数を揃える
  - 枝分かれを抑える
  - elementwise op を減らす
- split -> conv block → skip connection との concat → channel shuffle の構造を固定
  - conv block の部分を探索

## どうやって有効だと検証した？

- CIFAR-10 で ENAS と比較。test error を下げずに実行時間に約30%減

## 先行研究と比べて何がすごい？

- ENAS よりも早くてパラメータ数の少ないネットワークアーキテクチャを探し出した


## 議論はある

- ENAS よりも探索空間が少ない。このあたりは今後改善の余地あり
- 複数のパスが id になっている。パスを分けるのではなく和を重み付きにするといいのかも

## 次に読むべき論文
- N. Ma, X. Zhang, H. Zheng and J. Sun, “ShuffleNet V2: Practical Guidelines for Efficient CNN Architecture Design”, Arxiv, 1807.11164, 2018.
  - ShuffleNet V2 の論文
- H. Pham, M. Y. Guan, B. Zoph, Q. V. Le and J. Dean, “Efficient Neural Architecture Search via Parameter Sharing”, Arxiv, 1802.03268, 2018.
  - ENAS の論文
