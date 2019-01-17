GaussianProcesses.jl: A Nonparametric Bayes package for the Julia Language
===

2018/12/21 Jamie Fairbrother, Christopher Nemeth (Lancaster University), Maxime Rischard (Harvard University), Johanni Brea (EPFL)

https://arxiv.org/abs/1812.09064

（まとめ：[@antimon2](https://github.com/antimon2)）

---

## どんなもの？

+ ガウス過程のJuliag言語用パッケージの紹介
    + リポジトリ： https://github.com/STOR-i/GaussianProcesses.jl
+ できること（一例）：二値分類、時系列予測、数え上げ、ベイズ最適化

----

### ガウス過程

+ 機械学習以外にも様々な分野で使われている
+ 流行っている理由の1つが、各種数値計算言語で高品質なパッケージが公開されていてフリーで利用できるから
+ だからJulia用のパッケージも作った

---

## ~~先行研究~~ 他言語のパッケージと比べて何がすごい？

+ GPML: MATLAB用パッケージ（一部C言語で実装）
+ GPy: Python用パッケージ（一部Cythonで実装）
+ GPflow: Tensorflow ベースの実装
+ GaussianProcesses.jl: pure Julia
    + しかも速い！

---

## 技術や手法の肝は？

+ Julia の特徴として：
    + JITコンパイルによる高速・高効率な動的コード生成
    + 多重ディスパッチ
    + 既存の他のパッケージとの組合せ

---

## どうやって有効だと検証した？

+ GPML/GPy とベンチマーク比較し、全てにおいて最高速  
  ![Table1. - https://arxiv.org/pdf/1812.09064.pdf](https://i.imgur.com/X003Roe.png)

---

## 議論はある？

+ 以下の機能を開発中
    + 変分近似（Variational approximations）
    + 疎ガウス過程（Sparse Gaussian processes）
    + 自動微分（Automatic differentiation）

---

## 次に読むべき論文は？

+ 特になし
