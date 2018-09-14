BDD100K: A Diverse Driving Video Database with Scalable Annotation Tooling
===

2018/05/12 Fisher Yu, Wenqi Xian, Yingying Chen, Fangchen Liu, Mike Liao, Vashisht Madhavan, Trevor Darrell

https://www.arxiv-vanity.com/papers/1805.04687/

まとめた人: yuji38kwmt

---

## どんなもの？

* スケーラブルにアノテーションできるツールを、設計・実装した。
* このツールで、ドライビングデータセットを作成した

---

## 先行研究と比べて何がすごい？

* 既存ツールにある原始的なポリゴンで囲む機能だけでなく、ベジエ曲線や、隣接した線をコピーする機能をサポートしている
* 様々な種類のアノテーション（バウンディングボックス、セグメンテーション）が利用できる


---


## どうやって有効だと検証した？

* 半自動アノテーションで、バウンディングボックスのラベル付け時間が60％削減された（Fig3a)
* 隣接した線をコピーする機能によって、ポリゴンの作成時間が平均で36%減った（label 20 images with 842 polygons）

![Distribution of time in seconds spent on drawing a new bounding box and adjusting a bounding box suggested by the object detection model.](https://arxiv-sanity-sanity-production.s3.amazonaws.com/render-output/385408/images/time.png)
![Distribution of time in seconds spent on drawing a polygon one by one, and using copying boundaries. ](https://arxiv-sanity-sanity-production.s3.amazonaws.com/render-output/385408/images/copy_border.png)


---

## 技術や手法の肝は？

* ベジエ曲線でアノテーション
* 隣接した線のコピー機能

![隣接した線のコピー](https://arxiv-sanity-sanity-production.s3.amazonaws.com/render-output/390220/images/border_example.jpg)
![ベジエ曲線](https://arxiv-sanity-sanity-production.s3.amazonaws.com/render-output/390220/images/beizer/beizer_with.png)

---

## 議論はある？

* 特になし




---

## 次に読むべき論文は？

* [CFENet: An Accurate and Efficient Single-Shot Object Detector for Autonomous Driving](https://arxiv.org/abs/1806.09790)
* [Annotating Object Instances with a Polygon-RNN](https://arxiv.org/abs/1704.05548)

