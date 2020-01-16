Indoor Layout Estimation by 2D LiDAR and Camera Fusion
===

2020/01/15 Jieyu Li, Robert L Stevenson; University of Notre Dame

https://arxiv.org/abs/2001.05422

（まとめ：[@antimon2](https://github.com/antimon2)）

---

## どんなもの？

+ 前方画像（写真）と 2D LiDAR の組み合わせによる屋内レイアウトの推定（と再構築）。
+ 画像からの学習は**しない**

----

### 構成

+ LiDARデータセグメンテーション
+ ラインフィーチャ検出
+ 床-壁境界推定
+ 3D再構成

----

![Fig1](https://i.imgur.com/HvBwvTg.png)

---

## 先行研究と比べて何がすごい？

+ カメラのキャリブレーション情報不要
+ 画像だけの推定より簡単で正確

---

## 技術や手法の肝は？

+ 2D LiDAR（床面と平行にスキャン）とカメラの相対位置を固定
+ トップダウンビュー投影
+ R-RANSACアルゴリズム

---

## どうやって有効だと検証した？

+ 2つのデータセットで実験：
    + [Michigan Indoor Corridor Dataset](https://deepblue.lib.umich.edu/data/concern/data_sets/3t945q88k)
    + 自前データ（ノートルダム大学内で取得）

----

![Table1](https://i.imgur.com/WMfgrmb.png)

---

## 議論はある？

+ Discussion 節はないけれど…全体的に
    + 「整った空間できれいなデータが取れれば簡単に推定できるよ」としか言っていないような気がする
    + 設置物や落下物がたくさんあったり壁がない空間だったらとたんに破綻しそう

---

## 次に読むべき論文は？

+ [RoutedFusion: Learning Real-time Depth Map Fusion](https://arxiv.org/abs/2001.04388)
    + 2日前にsubmitされた似たようなテーマの論文
    + こちらはニューラルネットベースの話
