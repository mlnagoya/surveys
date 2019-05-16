Semantic Instance Segmentation with a Discriminative Loss Function
===

2017/08/08 Bert De Brabandere, Davy Neven, Luc Van Gool

https://arxiv.org/abs/1708.02551

（まとめ：[@antimon2](https://github.com/antimon2)）

---

## どんなもの？

+ Instance Segmentation の基本
    + **Discriminative Loss**（日本語だと **弁別的損失** ？）の利用
+ Tensorflow による実装 → https://github.com/hq-jiang/instance-segmentation-with-discriminative-loss-tensorflow

----

![Figure.1](https://i.imgur.com/gx04hCX.png)

---

## 技術や手法の肝は？

+ 入力画像の各画素を n-次元空間に埋込  
  （n＝2 or 3 くらい）
+ **Discriminative Loss**
    + (1) 分散項：クラスタ内引力
    + (2) 距離項：クラスタ間斥力
    + (3) 正則化項
    + (4) (1)～(3) の線型和（⇒損失関数）

----

![Figure.2](https://i.imgur.com/TLlq1TA.png)

----

![Equation.1~4](https://i.imgur.com/qIrMHNZ.png)

---

## どうやって有効だと検証した？

+ CVPPP, CityScape で実証

----

![Figure.5](https://i.imgur.com/g98EE40.png)

----

![Figure.6](https://i.imgur.com/jIEQhGW.png)

---

## 議論はある？

+ 速度と精度（とメモリ使用量）のトレードオフ
    + 精度重視ならResnet38（ただしメモリ爆食い）
    + 速度重視ならENet（省メモリ）

----

![Table.4](https://i.imgur.com/WAxkZoN.png)

---

## 先行研究と比べて何がすごい？

+ ProposalBasedじゃない
    + マルチステージじゃない
+ 回帰使わない
    + 単純で実装も容易
+ 離散表現・変換等しない
    + アドホックじゃない

---

## 次に読むべき論文は？

+ [Deep Semantic Instance Segmentation of Tree-like Structures Using Synthetic Data](https://arxiv.org/abs/1811.03208)
    + すでに読まれている → [第8回 by 陸さん](https://github.com/mlnagoya/surveys/blob/master/20181115_reports/Deep_Semantic_Instance_Segmentation_of_Tree-like_Structures_Using_Synthetic_Data/README.md)
+ [3D Graph Embedding Learning with a Structure-aware Loss Function for Point Cloud Semantic Instance Segmentation](https://arxiv.org/abs/1902.05247)
    + 3D点群データに対する Instance Segmentation
