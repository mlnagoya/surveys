Scale-Aware Trident Networks for Object Detection
===
Yanghao Li, Yuntao Chen, Naiyan Wang, Zhaoxiang Zhang

[paper](https://arxiv.org/abs/1901.01892)

@cohama


## どんなもの?

- 物体検出のための新しい (2-stage 用) Feature Pyramid 構築の提案
- Dilated Conv を使う
- FPN より多少マシな精度
- ICCV 2019

## 先行研究と比べて何がすごい？

- Image Pyamid はつらい
- Feature Pyramid はスケールごとに違う構造をつかっているので Image Pyramid の代替にならない

## 技術や手法の肝は？

- ResNet の Block の一部を dilation rate ごとに並列にするだけ。
  - dilation rate 1, 2, 3 ブランチがあり、それが N 個スタックする
  - 各ブランチは dilation rate のみ異なり、重みはシェアされる
- Scale-aware training (SNIP(ER) と同じ?)

## どうやって有効だと検証した？

- ResNet-101 backbone Faster R-CNN について、TridentBlock を入れたものとそうでないものを比較。COCO test-dev で mAP 37.9 → 40.6

## 議論はある?

- 本質的になんかすごいという感じではない
- dilation 3 のやつ Stack させると Receptive Field がでかくなりすぎるような気がするが良いのか。
  - conv2 や 3 から分岐させる精度低下するらしい

## 次に読むべき論文
- FPN: Tsung-Yi Lin, Piotr Doll ar, Ross B Girshick, Kaiming He,Bharath Hariharan, and Serge J Belongie. Feature pyramidnetworks for object detection. InCVPR, 2017.
- SNIP: Bharat Singh and Larry S Davis. An analysis of scale in-variance in object detection–SNIP. InCVPR, 2018.
- SNIPER: Bharat Singh, Mahyar Najibi, and Larry S Davis. SNIPER:Efficient multi-scale training. InNIPS, 2018.
