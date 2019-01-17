DetNet: A Backbone network for Object Detection
===

Zeming Li, Chao Peng, Gang Yu, Xiangyu Zhang, Yangdong Deng, Jian Sun


[paper](https://arxiv.org/abs/1804.06215)

@cohama


## どんなもの?

- Detection に用いる特徴抽出に特化したネットワークを考えた

## 技術や手法の肝は？

- 深い層では Pooling をいれず、Dilated Conv をつかう
  - Feature Map の解像度を変えないようにする
- ステージが変わるところでは Skip Connection のところに 1x1 Conv を入れる

## どうやって有効だと検証した？

- FPN 検出器で Backbone を ResNet-50 にしたときと DetNet にしたときで比較
  - mAP 40.2% (+3 point)
- IOU 85% 以上の評価のときに大きい物体の mAP が大きく向上 (+7 point)


## 先行研究と比べて何がすごい？

- 検出に特化した Backbone をちゃんと考えた？


## 議論はある?

- あまり被参照がないのは気になる


## 次に読むべき論文

- https://arxiv.org/abs/1809.02165
  - Object Detection のサーベイ
- https://arxiv.org/abs/1705.09914
  - Dilated ResNet
