## Recurrent Autoregressive Networks for Online Multi-Object Tracking

##### まとめ：　陸　衛強 (ろく　わいけん) 
##### https://github.com/wkluk-hk

---
+ Kuan Fang(1), Yu Xiang(2), Xiaocheng Li(1), Silvio Savarese(1)

	1.Stanford University, 2.University of Washington

+ Submitted on 7 Nov 2017 (v1), last revised 4 Mar 2018 (this version, v2)
+ https://arxiv.org/abs/1711.02741

---

### どんなもの？

+ 対象： MOT(Multi-Object Tracking)問題
+ 物体軌跡を任意長の時系列として扱い、時系列手法
	+ Autoregression (自己回帰モデル)
	+ GRU (Gated Recurrent Unit, RNNの一種)
 
 を組み合わせて、物体軌跡を生成
+ 名付けて 「Recurrent Autoregressive Network (RAN)」

---
### 先行研究と比べてどこがすごい？

+ MOTのよくあるアプローチ “tracking-by-detection” 
	+ MOT = 「個別フレームの検出器」+ 「フレーム間検出結果同士をつなげるアルゴ」
+ 「つなげるアルゴ」の入力は大体「見た目」と「位置」。出力は「位置の時系列」
+ RNNで「つなげるアルゴ」を作る試みはあったが、「見た目空間の複雑さ」>>>「訓練データセットサイズ」で訓練困難
+ RANの場合
	+ 外部メモリ（後述）で過去特徴を持ち続けるのでocclusionや検出ミスに強い
	+ 軌跡そのものではなく、Autoregressionのパラメータが出力だから訓練しやすい

---

### 技術や手法の肝は？

#### まず、自己Autoregression（自己回帰モデル)

![1](20180712_reports/Recurrent_Autoregressive_Networks_for_Online_Multi-Object_Tracking/assets/image/ScreenShot2018-07-05at11.44.25.png)

+ Xは、「見た目」や「位置」を表すベクトル。εは標準偏差σのホワイトノイズ
+ このモデルで、過去K FrameのXから次のFrameを推定して、実際のDetection結果と突き合わせる
+ ここのαとσはどうやって決めるか？
+++

#### Autogressionパラメータ（α,σ）はRNN(GRU)の出力

![2](20180712_reports/Recurrent_Autoregressive_Networks_for_Online_Multi-Object_Tracking/assets/image/ScreenShot2018-07-05at12.08.23.png)

+++

+ internal memoryを持つRNN Unit (LSTMの簡単版？）
+ INとなるのは、やはり「見た目」や「位置」の時系列
+ ｈ(チルダ付き），ｒ，ｚはすべて IN の Full Connect Layer で制御
+ 出力としてhidden層のhを得る
+ このhに、Full Connect Layerをつないで 先程のAutogressionのパラメータを出す

+++

#### 一枚の絵にすると

![3](20180712_reports/Recurrent_Autoregressive_Networks_for_Online_Multi-Object_Tracking/assets/image/ScreenShot2018-07-05at13.17.07.png)

+「見た目」特徴：実験ではinception networkのperson classifierから取得

---

## どうやって有効だと検証した？

### 精度評価
+ RAN(AR+RNN)を単純化した手法 (例：ARしないでRNNだけ、パラメータ固定のARなど)とのMOT精度評価でRANが勝つ

+++

+ MOT Benchmarkとの比較でも、一部指標で今のstate-of-the-artに勝つ

![4](20180712_reports/Recurrent_Autoregressive_Networks_for_Online_Multi-Object_Tracking/assets/image/ScreenShot2018-07-05at13.47.13.png)

+++

+ RNNの出力パラメータを見て、occlusionに強いことを確認
25番の人に対する、見た目特徴 Autogressionパラメータの変化

![5](20180712_reports/Recurrent_Autoregressive_Networks_for_Online_Multi-Object_Tracking/assets/image/ScreenShot2018-07-05at13.59.47.png)

---

## 議論はある？
+ とくにない

---


## 次に読むべきタイトルは？

とくにないが、参考情報として... 

##### MOT系のBenchmark
https://motchallenge.net/results/MOT16/?det=All

今の state-of-the-art MOTAは 70%超えている。

[参考動画](https://motchallenge.net/vis/MOT16-03/HT_SJTUZTE)

