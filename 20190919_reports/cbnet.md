CBNet: A Novel Composite Backbone Network Architecture for Object Detection
===

Yudong Liu, Yongtao Wang, Siwei Wang, TingTing Liang, Qijie Zhao, Zhi Tang, Haibin Ling

[paper](https://arxiv.org/abs/1909.03625)

@cohama


## どんなもの?

- 物体検出のための Backbone ネットワークを提案
- Cascade R-CNN と組み合わせることで、COCO test-dev において MegDet をも上回る精度 (mAP 53.3%) で No.1 達成
- ImageNet で訓練した Backbone を複数組み合わせ高レベルな特徴と低レベルな特徴をうまく混ぜ合わせる

## 先行研究と比べて何がすごい？

- 多くの物体検出器の Backbone は画像分類用のやつの流用なのでタスクに適しているとは言えない
- DetNet や FishNet など専用に考案されたアーキテクチャもあるが、これらは別途 ImageNet の pretrain が必要なので大変

## 技術や手法の肝は？

- 複数の Backbone を組み合わせる構成
  - ImageNet pretrain 済みの Backbone を K 個用意する (それぞれ Bk で表す)
  - Bk の l 番目のステージ (解像度が同じ層をまとめたもの) を Bk+1 の l-1 番目のステージの入力に混ぜる
  - 混ぜ方は 1x1 Conv → Upsampling
  - 最後の Backbone の各ステージの出力を FPN の入力とする
  - K は2か3くらい

## どうやって有効だと検証した？

- 自前で用意した FPN、Mask R-CNN、Cascade R-CNN に対して backbone を CBNet に置き換えた場合の COCO test-dev mAP で評価
    - Flip のデータオーグメンテーションだけ
    - Multiscale testing で MegDet を上回る mAP 53.3%
- 接続の仕方や最適な K についても Ablation study で調査
- パラメータを共有したり、浅い層を削ったりすることでサイズ/速度を改善できる
- 有効性を確認するために途中の層の出力の可視化も行った。
  - 背景の出力が抑えられ、物体のある部分がより強調されたような Feature map になっている

## 議論はある?

- レベルの違う特徴を混ぜ合わせるという意味では FPN、PANet、M2Det などで試みられているが Backbone の時点でそれをするほうがいいということなのか。
  - FishNet は似ているようだが同じレベルの特徴を混ぜるのがよくない

## 次に読むべき論文
- MegDet: A Large Mini-Batch Object Detector (https://arxiv.org/abs/1711.07240)
- M2Det: A Single-Shot Object Detector based on Multi-Level Feature Pyramid Network (https://arxiv.org/abs/1811.04533)
- DetNet: A Backbone network for Object Detection (https://arxiv.org/abs/1811.04533)
- FishNet: A Versatile Backbone for Image, Region, and Pixel Level Prediction (https://arxiv.org/abs/1901.03495)
