The ParallelEye Dataset: Constructing Large-Scale Artificial Scenes for Traffic Vision Research
===

2017/12/22 Xuan Li, Kunfeng Wang, Member, IEEE, Yonglin Tian, Lan Yan, and Fei-Yue Wang, Fellow, IEEE

https://arxiv.org/pdf/1712.08394.pdf
https://www.arxiv-vanity.com/papers/1712.08394/

（まとめ：yuji38kwmt）

---

## どんなもの？
* [ParalellEye](http://openpv.cn/datasets/paralleleye/)という画像データセットの説明
* 作り方
    1. 地図データから、北京中関村（Zhongguancun ）の3D Modelを作成
    2. Then, we use the computer graphics, virtual reality, and rule modeling technologies to create a realistic, large-scale virtual urban traffic scene, in which the fidelity and geographic information can match the real world well.
    3. シーンレンダリング、自動的なアノテーションを実施するために、Unity3D開発環境を使う
        * ground truth labels including pixel-level semantic/instance segmentation, object bounding box, object tracking, optical flow, and depth.

---

## 先行研究と比べて何がすごい？

* Unity3Dを使うことにより、正確（主観的でない）で効率的なアノテーションが可能
* 人がアノテーションするときの問題
    * ビデオ画像データセットのアノテーションは時間がかかる。間違えやすい
    * 専門家はsparse
    * 意見が一致しないとき、どう対応するか
    * アノテーションは時間がかかる30-60分
* [virtual KITTI](http://www.europe.naverlabs.com/Research/Computer-Vision/Proxy-Virtual-Worlds)は、拡張できない
* 多くのデータセットはセマンティックセグメンテーションアノテーションを提供していない

---

## どうやって有効だと検証した？
* 車の屋根に載せたカメラ
![車載カメラ](https://arxiv-sanity-sanity-production.s3.amazonaws.com/render-output/419252/x7.png)

* 監視カメラ
![監視カメラ](https://arxiv-sanity-sanity-production.s3.amazonaws.com/render-output/419252/x8.png)

---

## 技術や手法の肝は？

* Parallel Vision
    * ACP(Artificial Systems、Computational Experiment、Parallel Execution)
    * よくわからなかった
* [OpenStreetMap(OSM)](https://www.openstreetmap.org/#map=6/35.588/134.380)で、都市のネットワークを抽出
* CityEngineはCGA（Computer Generated Architecture）ルールの作成、または人工的なシーン（道路、建物、車、樹木、歩道など）の設計に使われる
* 人工的なシーンは、Unity3Dに取り込まれ、レンダリングされる
* Unity3Dは環境条件の制御のために使われる

![Pipeline for generating the ParallelEye dataset with OpenStreetMap, CityEngine, and Unity3D.](https://arxiv-sanity-sanity-production.s3.amazonaws.com/render-output/419252/x3.png)



---

## 議論はある？
Discussionなし。

感想
* ParalellEyeデータセットを使って学習したらうまくいく？




---

## 次に読むべき論文は？


* [Joint Semantic Segmentation and 3D Reconstruction from Monocular Video](https://smartech.gatech.edu/bitstream/handle/1853/53675/HybridSFM-ECCV14.pdf?sequence=1&isAllowed=y)
    - アノテーション時間に関して書いてある？
* [Semantic Instance Annotation of Street Scenes by 3D to 2D Label Transfer](http://www.cvlibs.net/publications/Xie2016CVPR.pdf)
    - "curse of dataset annoation"のグラフあり


=======================
---

### 用語
* ACP (Artificial systems, Computational experiments, and Parallel execution) theory
* Optical Flow
* Parallel Vision?
* optical flow, and depth

### 豆知識
* virtual datasetの歴史は古い 2007年？
* セマンティックセグメンテーション：10-20カテゴリ、高品質、1枚：30-60分
* “curse of dataset annotation” : データセットの呪縛？
* Google Mapsはオープンソースでない
