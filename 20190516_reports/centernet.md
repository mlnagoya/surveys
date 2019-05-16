CenterNet: Keypoint Triplets for Object Detection
===

Kaiwen Duan, Song Bai, Lingxi Xie, Honggang Qi, Qingming Huang, Qi Tian

[paper](https://arxiv.org/abs/1904.08189)

@cohama


## どんなもの?

- 通常の物体検出とは異なり、Anchor ではなくキーポイントから物体を検出
- 既存の CornerNet にさらに中心を予測させるような枝を追加
- COCO mAP 47%、340 msec/image

## 技術や手法の肝は？

- CenterNet をベースにしている
  - 左上の点と右下の点のヒートマップを予測
  - ヒートマップのピクセルから実際の枠の位置までのオフセットを回帰で予測
  - 同じ物体だと同じ、違う物体に対しては違うベクトルを出すような Embedding
  - コーナーのヒートマップに適した Pooling 手法 (Corner Pooling)
- CenterNet ではさらに以下を追加
  - 中心点のヒートマップ
  - 中心点に適した Center Pooling
  - より中心の情報を使うよう改良した Cascade Corner Pooling
  - コーナーと中心が同じラベルで予測され、近い距離の Embedding を出力し、かつ、中心がちゃんと中心
    (コーナーで作られた枠の1/3か1/5くらいのずれの範囲に収まっているか)

## どうやって有効だと検証した？

- COCO でテスト
  - single-scale 44.9%, multi-scale 47.0%
- 中心点キーポイント、Center Pooling、Cascade Corner Pooling のそれぞれの効果を確認


## 先行研究と比べて何がすごい？

- 精度があがった！

## 議論はある?

- 47.0% すげーと思ったら multi-scale testing だった
  - single 44.9% もまぁまぁすごいけど
- 中心キーポイントがちゃんと中心にあるかの判定が雑だけどこれでいいのか


## 次に読むべき論文
- L. Tychsen-Smith and L. Petersson. Denet: Scalable real-time object detection with directed sparse sampling. InPro-ceedings of the IEEE International Conference on ComputerVision, pages 428–436, 2017.
- https://arxiv.org/abs/1706.03646
- CornerNet https://arxiv.org/abs/1808.01244
  - 左上と右下の2点のキーポイント検出と、それらが同一物体のペアになるかを推論
- CornerNet-Lite https://arxiv.org/abs/1904.08900
