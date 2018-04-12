Employing Weak Annotations for Medical Image Analysis Problems
===

Submitted on 2017/08/21
by Martin Rajchl a, Lisa M. Koch a, Christian Ledig a, Jonathan Passerat-Palmbach a, Kazunari Misawa b, Kensaku Mori c, Daniel Rueckert a
* a. Dept. of Computing, Imperial College London, UK
* b. Aichi Cancer Center, Nagoya, JP
* c. Dept. of Media Science, Nagoya University, JP

Subjects: Computer Vision and Pattern Recognition (cs.CV)

https://arxiv.org/abs/1708.06297

論文紹介 by github.com/exoego

---

# どんなもの？

## 背景

* 医療分野でComputer Vision用データセットの需要が高まっているが、医療専門家は限られていてアノテーションの調達が難しい。
* そこそこの質のアノテーションを大量に安く作成するため、他分野と同様にクラウドソーシング（Mechanical Turkなど）を活用したい。
* 矩形アノテーションの作成は、ピクセルレベルの高品質セグメンテーションアノテーションより15倍速い、と報告されている。

## 動機

Weakアノテーション（医療専門知識のない人がつけた、エラーがあるかもしれないアノテーション）を機械学習に活用し、十分な精度のセグメンテーションをしたい。

## 貢献

* CTスキャンの3次元セグメンテーションタスクに使う2次元（断面）アノテーションから、低品質なアノテーションを除外するアルゴリズムを提案する。
* この手法で非専門家の作ったエラーを含むアノテーション（Weak Annotation）でも、専門家によるアノテーションを使った場合に匹敵する精度を得られた。

### 専門知識（エラーの少なさ）の影響

* 専門知識＝解剖学的知識が求められる対象を正確に見つけられる割合＝エラーの少なさ、と定義。
* エラー率が高いほど精度が下がるのは予想通り。

考察
1. たとえエラー率は低くても、エラーのあるアノテーションの絶対量が多いほどセグメンテーション精度が落ちる可能性が示唆された。
	* エラー率が高い状況では、アノテーションの絶対量を増やせない……
2. 提案手法でエラーの多いアノテーションを除去することで、特にRR（矩形）でエラー率が50%と高くても90%以上のセグメンテーション精度が得られた。
	* 従来、専門知識が必要だった領域でも、クラウドソーシング活用の可能性が出てきた。


実験結果:
![実験結果](https://image.ibb.co/ekw6xH/2018_04_12_180310.jpg)
![セグメンテーションの例](https://image.ibb.co/mdWvrc/2018_04_12_175724.jpg)


---

## どうやって有効だと検証した？

専門家が作った精密なセグメンテーションをベースに、「非専門家が作った風」のアノテーションをシミュレーションで生成。
生成したのアノテーションをもとにセグメンテーションして、定量評価した。

* 元画像：名大病院提供150人分の腹部CTスキャン。立体イメージから断面画像を得る。X/Y/Z 3方向同僚ずつ。
* 前処理：専門家が作ったアノテーションから、異なる種類のアノテーションを、アノテーション率（間引き率）・エラー率ごとに生成。	
* 立体セグメンテーション手法：生成したアノテーションを合成して得た空間アノテーションを用い、PSと同じmax-flow solverを使用（GPU使えて速いので）。
* 評価：パラメータ組合せ（アノテーション率7 * エラー率5 * 3アノテーション種類）* 20画像/実験 = = 2100セグメンテーションについて、エラー除去前/後で評価。

![アノテーションの種類](https://image.ibb.co/i3Mjjx/2018_04_12_175818.jpg)

## 技術や手法の肝は？

エラーのあるアノテーションの除去

### flawed and weakly labelled atlas（不完全でエラーのある可能性があるラベル地図）

* 動機：weakアノテーションしかない状況でも、低品質（誤検出、見落し）アノテーションを自動検知したい。
* 手法：
	* 医療分野でよく用いられるMAS（multi-atlas segmentation）と同じ考えで、解剖学的（空間的）に類似した断面画像とそこにつけられたアノテーションを検索。
		* 類似度は、二乗誤差和などの手法で計算。
	* 抽出された断面群をラベルフュージョンし、合意アノテーションO1を作成。
	* この合意アノテーションとの重なりを、個々のアノテーションの精度DSCとして計算）。「合意アノテーションO1に対する平均DSC」よりもDSCが低いアノテーションを除外する。

![DSCイメージ](https://image.ibb.co/knp4jx/2018_04_12_180321.jpg)

---

## 先行研究と比べて何がすごい？

* エラーアノテーションを除去するにあたり、事前に専門家がつけた高品質アノテーションを必要としない。
	* →データセットがまだない領域にも使えるかも？

---

## 議論はある？

* 分野固有の手法を使わず、一般的なmax-flowセグメンテーションを使っているのは大丈夫？　逆に一般性があってよい？


---

## 次に読むべき論文は？

アノテーションへのクラウドソーシング活用の先行研究（個人的な興味）

+ Estell´es-Arolas, E., Gonz´alez-Ladr´on-De-Guevara, F., 2012. Towards　an integrated crowdsourcing definition. Journal of Information science　38, 189–200
* Albarqouni, S., Baur, C., Achilles, F., Belagiannis, V., Demirci, S., Navab, N., 2016. Aggnet: Deep learning from crowds for mitosis detection in breast cancer histology images. IEEE transactions on medical imaging 35, 1313–1321.
