Deformable Convolutional Networks
===

Jifeng Dai, Haozhi Qi, Yuwen Xiong, Yi Li, Guodong Zhang, Han Hu, Yichen Wei

[paper](https://arxiv.org/abs/1703.06211)

@cohama


## どんなもの?

- 通常の畳込みは隣接の3x3など予め決まった位置のピクセルの値で畳み込みを行うが、これを自由な位置を参照できるように改良した Deformable Convolution という手法を提案
- Atrous Convolution の一般化
- 同様に ROI Pooling も自由な位置を参照する版の Deformable ROI Pooling も提案
- 物体検出タスクで +2 ~ +5% ほどの精度向上

## 技術や手法の肝は？

- Deformable Convolution
  - 入力のフィーチャーマップから x, y 方向のオフセットのマップを作るための畳込みを行う
  - オフセットマップと入力のフィーチャーマップから線形補間したフィーチャーマップを作る
  - 畳み込む
- Deformable ROI Pooling

- Deformable Convolution は最終層直前に3層くらいいれるのがよい


## どうやって有効だと検証した？

- Segmentation (PASCAL VOC, Cityscapes)
  - mAP +5%
- Object Detection (PASCAL VOC, COCO)
  - どのアーキテクチャでも mAP +3% くらい


## 先行研究と比べて何がすごい？

- インスタンスごとに最適な Receptive Field をもてる。すごい
- 簡単で汎用性が高いのでほかのアーキテクチャにも応用ができる
- そんなに遅くない

## 議論はある?

- 途中の層に入れないのか？

## 次に読むべき論文
- Deformable Conv v2 https://arxiv.org/abs/1811.11168
