Gen: A General-Purpose Probabilistic Programming System with Programmable Inference
===

2019/06/22 Marco F. Cusumano-Towner, Feras A. Saad, Alexander K. Lew, and Vikash K. Mansinghka - [MIT](https://dl.acm.org/inst_page.cfm?id=60022195)

https://doi.org/10.1145/3314221.3314642

（まとめ：[@antimon2](https://github.com/antimon2)）

---

## どんなもの？

+ 汎用確率プログラミングシステム [Gen](https://probcomp.github.io/Gen/) の紹介。
    + [Source](https://github.com/probcomp/Gen) on GitHub

----

![Figure 1. Comparison of Gen’s architecture to a standard probabilistic programming architecture.
](https://i.imgur.com/vpiatZX.png)  

---

## 技術や手法の肝は？

+ [Julia](https://julialang.org/) ベースで、高速かつ汎用
+ Generative Function
    + 確率モデルをカプセル化
+ 相互運用可能なモデリング言語
    + 柔軟性と効率の両立
+ 抽象化された推論ライブラリ
    + 効率的なアルゴリズムをプラグイン

---

## どうやって有効だと検証した？

+ いくつか実装例を挙げている：
    + Object Tracking
    + 3D Body Pose Inference
    + Time Series Structure Estimation

----

![Figure 5a. body pose inference](https://i.imgur.com/BIWJtI7.png)

---

## ~~先行研究~~ 他のプロダクト と比べて何がすごい？

+ あるプロダクト：特定のドメインに特価した制限付きモデリング言語
    + → Gen は汎用的
+ あるプロダクト：ユニバーサルモデリング言語を提供するが限られた推論アルゴリズムセットのみをサポート（しかも遅い）
    + → Gen は高速

---

## 議論はある？

+ ※特になし

---

## 次に読むべき論文は？

+ …
