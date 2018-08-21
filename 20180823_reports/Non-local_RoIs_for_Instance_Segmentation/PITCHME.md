## Non-local RoIs for Instance Segmentation

##### まとめ：　陸　衛強 (ろく　わいけん) 
##### https://github.com/wkluk-hk

---
+ Shou-Yao Roy Tseng[1], Hwann-Tzong Chen[1], Shao-Heng Tai[2], Tyng-Luh Liu[3]
	+ 1.National Tsing Hua University, 2.Umbo Computer Vision, 3.Academia Sinica
+ Submitted on 14 Jul 2018
+ https://arxiv.org/abs/1807.05361

---

### どんなもの？

+ 対象問題： Instance segmentation
+ Mask R-CNNの拡張として、「Non-local RoI Block」というnetwork blockを提案

---
### 先行研究と比べてどこがすごい？

+ 先行研究：Faster R-CNN or Mask R-CNN
	+ 2 stage方式の object detecion
		+ stage 1: object region proposalsでN個のRoIを出す (region of interest)
		+ stage 2: RoIごとに 分類/B-BOXの回帰/Segmentation
	
![1](20180823_reports//Non-local_RoIs_for_Instance_Segmentation/assets/image/Screen_Shot_2018-08-20_at_14.59.00.png)



+++

+ stage2はRoI別で処理されるが、segmentation問題において重要なハズの離れた他のRoI情報は、stage 2のnetworkにほぼ伝わってこない
+ Non-local RoI BlockでRoI同士をつなげるアーキを提案してそれを改善した
+ Robust Vision Challengeの[Instance Segmentation Leaderboard](http://www.robustvision.net/leaderboard.php?benchmark=instance)や[Kitti](http://www.cvlibs.net/datasets/kitti/eval_instance_seg.php?benchmark=instanceSeg2015)で現在２位

---

### 技術や手法の肝は？

Mask R-CNNの Stage1 と Stage2の間に以下のBlockを挟むだけ

#### Non-Local RoI Block（数式)

![2](20180823_reports//Non-local_RoIs_for_Instance_Segmentation/assets/image/Screen_Shot_2018-08-20_at_15.02.42.png)

+ i や jは、RoIを表す(Mask R-CNNのstage1の出力、全部N個)
+ xは、RoIが持っているfeature vector. shapeは(D , H , W) 
+ g(x_j) は、RoIが他RoIへ与える影響を表すvector関数 (BP学習対象)
+ f(x_i,x_j)は、２つのRoIの関連性を表すscalar関数 (BP学習対象)
+ C(X)は正規化項 (scalar関数)
+ yは、全RoIから受ける入力の合計
	+ xにくっつけて、先のMask R-CNNのstage2( segmentation/分類/枠の回帰とか)　に渡す

+++

#### 絵にした場合

![3](20180823_reports//Non-local_RoIs_for_Instance_Segmentation/assets/image/Screen_Shot_2018-08-20_at_15.16.10.png)

+++


#### 実際のf(x_i,x_j)、g(x_j)、C(X)の関数定義

![2](20180823_reports//Non-local_RoIs_for_Instance_Segmentation/assets/image/Screen_Shot_2018-08-20_at_15.02.42.png)

+ Non-Local Connectionの元ネタとなった論文で、いろいろな関数定義が試されている。結果的に、何を使っても対して変わらないらしい

+ ここでは、f(x_i,x_j)とC(X)は、いわゆるsoftmax関数を使う

![3](20180823_reports//Non-local_RoIs_for_Instance_Segmentation/assets/image/Screen_Shot_2018-08-20_at_15.22.19.png)

+ φ と  ψは、 1-by-1 2D convolution (チャネル数をDからD_fに落とすだけ)

+ g(x_j)は、 1-by-1 convolution -> 3-by-3 convolution -> average poolして最後は D_g次元のvectorを作る

+++ 絵にした場合

![4](20180823_reports//Non-local_RoIs_for_Instance_Segmentation/assets/image/Screen_Shot_2018-08-21_at_9.52.43.png)

---

## どうやって有効だと検証した？

### 精度評価
+ benchmarkあるのみ

---

## 議論はある？
+ とくにない

---


## 次に読むべきタイトルは？
####ほぼ本論文の元となった論文
+ [Non-local Neural Networks](https://arxiv.org/pdf/1711.07971.pdf)
	+ Non-local blockを提案。中身の関数をいろいろ試した結果など
	+ RNNに頼らないlong-range dependency modelingができ、video classification問題でstate-of-the-art

####self-attention応用いろいろ
+ 「Non-Local」な連携は、言語処理で盛り上がっている（らしい）self-attentionを汎化した形として捉えられる（本論文・元論文でも言及）
	
+ 「Non-Local」の数式 ![5](20180823_reports//Non-local_RoIs_for_Instance_Segmentation/assets/image/Screen_Shot_2018-08-21_at_10.00.33.png)
+ 「self-attention」の数式: ![6](20180823_reports//Non-local_RoIs_for_Instance_Segmentation/assets/image/Screen_Shot_2018-08-21_at_10.00.44.png)

+ 日本語論文解説 [Attention Is All You Need (Transformer)](http://deeplearning.hatenablog.com/entry/transformer)
+ Attention Networkの画像系活用
	+ [Residual Attention Network for Image Classification](https://arxiv.org/pdf/1704.06904.pdf)
	+ [Self-Attention Generative Adversarial Networks](https://arxiv.org/abs/1805.08318)
