Joint distribution optimal transportation for domain adaptation
===

NIPS2017

Nicolas Courty (Université de Bretagne Sud),  
Rémi Flamary (Université Côte d’Azur), 
Amaury Habrard (Univ Lyon, UJM-Saint-Etienne, CNRS), 
Alain Rakotomamonjy (Normandie Universite)


論文のリンク先URL : 
http://papers.nips.cc/paper/6963-joint-distribution-optimal-transportation-for-domain-adaptation.pdf

（まとめ：@matsui_kota）

---

## どんなもの？

+ 教師なしドメイン適応問題 : 元ドメインのラベルありデータを援用して目標ドメイン (ラベル情報なし) における予測モデル$f$を学習する
	+ 各ドメインで入力の周辺分布は共通, 入力と出力の同時分布が異なる

+ 仮定 : 元ドメインの同時分布$P_s(x, y)$と目標ドメインの同時分布$P_t(x, y)$の間にある非線形変換が存在し, 
それは最適輸送によって推定可能

+ 提案法 : カップリング測度と予測モデル$f$を同時に最適化する方法であり, この方法によって目標ドメインを$\mathcal{P}_t^f = (X, f(X))$で推定することができる

	+ 提案法は目標ドメインの誤差の上界を最小化していることに対応. アルゴリズムは収束性が保証されている.  

---

## どうやって有効だと検証した？

+ 2つの転移学習タスク (判別と回帰) で提案法の有効性を検証. 用いたdatasetは3つ (判別にCaltech-Office classification dataset と Amazon review classification dataset, 回帰にWifi localization regression dataset). 

+ Caltech-Office dataset (画像, 判別タスク)
	+ adaptationなし (baseline), surrogate kernel approach (Surk), subspace adaptation (SA), adaptation regularization (ARTL), entropy-regularized OT (OT-IT), classwise regularized OT (OT-MM) の6手法と提案法を比較
	+ 全転移シナリオの平均精度では提案法が最も良いパフォーマンス

+ Amazon review classification dataset (自然言語, 判別タスク)
	+ このタスクのSOTAであるDomain adversarial neural network (DANN) との比較
	+ 提案法がDANNを上回るパフォーマンスを示した

+ Wifi localization regression dataset (回帰タスク)
	+ 転移シナリオは transfer across periods (3時点) と　transfer across devices (3デバイス) の2パターン合計6通り
	+ kernel ridge regression (KRR), Surk, domain-invariant projection (DIP, DIP-CC), generalized target shift (GeTarS), conditional transferable components (CTC, CTC-TIP) の7手法と提案法を比較
	+ transfer across devices パターンでは全シナリオで提案法が優勝
　


---

## 技術や手法の肝は？
+ まず, joint distribution optimal transportの最適化問題は
\begin{align}
\min_{f, \gamma} \sum_{i, j}
\left[
\alpha {\mathrm d}(x_i^s, x_j^t) + 
\mathcal{L}(y_i^s, f(x_j^t)) 
\right]\gamma_{ij} + 
\lambda \Omega(f)
\end{align}
と書ける ($P_s$と$P_t^f$の$L_1$-Wasserstein距離$W_1(\hat{P}_s, {\hat{P}_t}^{f})$を$f$に関して最小化していることと同値). $\Omega$は正則化項. 

+ $f$と$\gamma$の最適化が分離できるので, 交互最適化可能 (ブロック座標降下法を適用)
	1. $f$を止めて$\gamma$を最適化. network simplex algorithmなど古典的な最適輸送のアルゴリズムで最適化可能
	2. $\gamma$を止めて$f$を推定. 回帰の場合は二乗損失最小化, 判別の場合はヒンジ損失最小化などで$f$推定する. $f$がRKHSの元であれば普通の最小二乗法や多クラスSVMの問題. 
+ 理論的には, 目標ドメインの汎化誤差$err_T(f)$は以下のようにboundされる : 
\begin{align}
err_T(f) 
\le W_1(\hat{P}_s, {\hat{P}_t}^{f}) + 
O(\frac{1}{\sqrt{N_s}} + \frac{1}{\sqrt{N_t}}) + 
err_S(f^*) + err_T(f^*) + O(\phi(\lambda))
\end{align} 
	+ 第1項は元ドメインの分布と目標ドメインの分布のWasserstein距離
	+ 第2項はサンプルサイズが大きくなると消えていく項
	+ 第5項はPTL条件 (予測モデル$f$と$P_s$, $P_t$のカップリング測度が持つべき性質. $f$がリプシッツ性を持たない確率が$phi(\lambda)$以下になる)の上界に依存する項
	+ 第3, 4項は, そもそも各ドメイン内で$f^*$による予測が上手くいかなければ転移学習も失敗するという気分を表す. 

---

## 議論はある？

+ Wifi localization regression datasetでの実験結果から, 元ドメインと目標ドメインの間の分布のズレが大きいほど最適輸送が有効に働くことが示唆
	+ reweighting methodやMMDなどでは捉えきれない 
+ 元ドメインのラベル無しデータも使う半教師あり設定への拡張, adaptationをより効率的に行うための確率的最適化法の導入などが今後考えられる
+ 理論的にはPTL条件のより詳細な解析, 汎化誤差boundに仮説空間の複雑さや輸送関数空間の複雑さを加味する, などが future work

---

## 先行研究と比べて何がすごい？

+ 従来の最適輸送ベースのドメイン適応手法は$P_s$と$P_t$との近似Wasserstein距離を最小にする重心写像を用いて$f$を推定していた (最適化ではない?) $\rightarrow$ 元ドメインから目標ドメインへの複雑な変換
+ 提案法は最適輸送を元ドメインから目標ドメインへのラベルプロパゲーションにのみ使用 ($f$の推定とは切り離している) しているため問題がシンプルになった
+ $L^p$距離の最適輸送の先行研究を含むようなより一般の問題設定になっている


---

## 次に読むべき論文は？

+ [Sinkhorn Distances: Lightspeed Computation of Optimal Transportation Distances](https://arxiv.org/abs/1306.0895)
    + 最適輸送を効率的に計算可能にした
    + ドメイン適応への応用のさきがけ
+ [Optimal Transport for Multi-source Domain Adaptation under Target Shift](https://arxiv.org/abs/1803.04899)
	+ 同じグループの最新論文
	+ target shift (ドメイン間でクラスバランスが変わる設定) に対してOTベースのドメイン適応手法を開発 
