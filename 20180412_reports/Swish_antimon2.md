Searching For Activation Functions
===

2017/10/27 Prajit Ramachandran, Barret Zoph, Quoc V. Le (Google Brain)

https://arxiv.org/pdf/1710.05941.pdf

（まとめ：[@antimon2](https://github.com/antimon2)）

---

## どんなもの？

+ ReLU に変わる新しいアクティベーション関数 **Swish** の紹介。
+ f(x) = x ⋅ sigmoid(βx) というシンプルな式。
+ ImageNet で ReLU を Swish に置き換えたら、正解率が 0.9% 向上した。
+ Swish 用に最適化されたハイパーパラメータ設定により、さらなる効果が期待できる。

---

## どうやって有効だと検証した？

+ Swish と ReLU、そして他のいくつかの活性化関数を用いて、以下の各種ネットワーク・タスクで検証：
    + CIFAR: 3種類のモデル、Accuracy を比較
    + ImageNet: 3種類のモデル、Accuracy を比較
    + 機械翻訳: 4種類のデータセット、BLEU を比較
+ 全てで Swish が最高（または最高タイ）の値を出したことを確認

---

## 技術や手法の肝は？

+ 数式が単純（f(x) = x ⋅ σ(βx)）
    + β = 0 ⇒ f(x) = x/2
    + β → ∞ ⇒ ReLU に漸近
+ f′(x) = βf(x) + σ(βx)(1 − βf(x))
+ （ReLU と異なり）**非単調** で **滑らかな関数**

---

## 議論はある？

+ ReLU の勾配保存特性の重要性に関する仮説は不要と思われる
    + Swish の $x<0$ の時の『下に凸』な部分（$f(x) < 0$ の部分）こそが重要という実験結果が出ている

---

## 先行研究と比べて何がすごい？

+ ほとんどの先行研究は、新しい活性化関数を提案することに焦点を当てているが、この研究では他の活性化関数との比較を系統的に行っている
+ この研究では Swish が deep model で一貫して ReLU より優れていることを示している

---

## 次に読むべき論文は？

+ [Learning transferable architectures for scalable image recognition.](https://arxiv.org/pdf/1707.07012.pdf)
    + 最適パラメータ（CNN）の検索技術
+ [Learning to reinforcement learn](https://arxiv.org/pdf/1611.05763.pdf)
    + 適応可能強化学習?


