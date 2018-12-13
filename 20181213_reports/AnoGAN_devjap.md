Unsupervised Anomaly Detection with Generative Adversarial Networks to Guide Marker Discovery
===

2017/3
Thomas Schlegl, Philipp Seeböck, Sebastian M. Waldstein, Ursula Schmidt-Erfurth, Georg Langs

[https://arxiv.org/abs/1703.05921](https://arxiv.org/abs/1703.05921)

（まとめ：@devjap）

---

## どんなもの？
+ GANによる画像の異常検知手法
+ 正常画像でトレーニングしたGeneratorは異常画像を再現できないと考え、異常画像を元に再生成した場合異常部分が生成されずに差分として検出ができるのではないかというアイディア


## どうやって有効だと検証した？
+ モデルが現実的な画像を生成できるかどうかを定性的に調べた。
  - 訓練データから、正常データをどれだけ精微に再現できるかが肝
+ モデルが異常を検知できるか定性的に調べた。
  - 異常な画像を入力とした場合に生成した画像との差が検知できるレベルにあるかが重要。
+ 異常な画像の場合、入力画像と生成された画像のペアは、明らかな強度またはテクスチャの違いを示す。

## 技術や手法の肝は？
+ 新しい画像を潜在空間にマッピングする（逆写像）
+ G,Dの重みは固定した状態でLossが最小になるZを勾配法で探す。
+ 作成された画像とオリジナルを比較してチェック

## 議論はある？
+ 画像一つ一つに対して勾配法でZを探すため検査に時間がかかる。（MNISTでも結構かかるくらいのレベル

## 先行研究と比べて何がすごい？
+ 正常データのみを使って異常箇所をアノテーションできる

## 次に読むべき論文は？
+ [EFFICIENT GAN-BASED ANOMALY DETECTION](https://arxiv.org/pdf/1802.06222.pdf)
  - Referenceではないが、効率よく生成画像を作るヒントになりそうな論文
