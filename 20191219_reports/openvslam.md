OpenVSLAM: A Versatile Visual SLAM Framework
===

2019/10/10 Shinya Sumikura, Mikiya Shibuya, Ken Sakurada
[https://arxiv.org/abs/1910.01122](https://arxiv.org/abs/1910.01122)

（まとめ：@nharu1san）

---
## どんなもの？
- オープンで利用しやすいVisual SLAMフレームワーク
- [https://github.com/xdspacelab/openvslam](https://github.com/xdspacelab/openvslam)

---
## 先行研究と比べて何がすごい？
![](./arxiv_1910.01122/table_1.png)
- ゆるいライセンス(二条項BSDライセンス)
- APIにまとめてあって使いやすい
- 魚眼, 全天球等のカメラタイプとも互換性がありカスタマイズ可能
  - 正距円筒画像を利用できる最初のOSS SLAMフレームワーク
- ブラウザで表示できるViewer

---
## 技術や手法の肝は？
![](./arxiv_1910.01122/fig_1.png)
- ORBで特徴点抽出

---

## どうやって有効だと検証した？
![](./arxiv_1910.01122/fig_2.png)
- EuRoC MAVとKITTI odometryについてORB-SLAMと比較

---

## 議論はある？
- 特に無し

---

## 次に読むべき論文は？
- [https://arxiv.org/abs/1502.00956](ORB-SLAM: a Versatile and Accurate Monocular SLAM System)
- [https://arxiv.org/abs/1709.04377](ProSLAM: Graph SLAM from a Programmer's Perspective)
- [https://arxiv.org/abs/1912.03426](Self-Supervised 3D Keypoint Learning for Ego-motion Estimation)