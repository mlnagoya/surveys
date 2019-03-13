DiffEqFlux.jl — A Julia Library for Neural Differential Equations
===

2019/02/06 Chris Rackauckas, Mike Innes, Yingbo Ma, Jesse Bettencourt, Lyndon White, Vaibhav Dixit

https://arxiv.org/abs/1902.02376

（まとめ：[@antimon2](https://github.com/antimon2)）

---

## どんなもの？

+ ニューラル微分方程式ソルバーライブラリの紹介
    + リポジトリ： https://github.com/JuliaDiffEq/DiffEqFlux.jl
    + サンプルコード： https://github.com/FluxML/model-zoo/tree/master/other/diffeq
    + 元のブログ記事： https://julialang.org/blog/2019/01/fluxdiffeq

----

### ニューラル微分方程式

+ 微分方程式とニューラルネットの統合
    + 微分方程式をニューラルネット（機械学習）で解く
    + 逆にニューラルネットを微分方程式に組み込む(?)

---

## 技術や手法の肝は？

+ ニューラルネットの層とは、入力として長さ `n` のベクトルと受け取り、長さ `m` のベクトルを出力する、*微分可能な関数*。
    + (O)DEソルバーもその条件を満たす！
    + それを利用して(O)DEを解く！
+ Julia のエコシステムでそれらを同時に利用できるようにマージした。

----

### DiffEqFlux.jl

+ [DifferentialEquations.jl](https://github.com/JuliaDiffEq/DifferentialEquations.jl) で用意されている様々な微分方程式モデルを利用したレイヤを [Flux.jl](https://github.com/FluxML/Flux.jl/) に簡単に組み込める！
    + 硬い常微分方程式（Stiff ODE）
    + 確率微分方程式（SDE）
    + 遅延微分方程式（DDE）
    + ハイブリッド（不連続）微分方程式

---

## ~~先行研究~~ 他言語のパッケージと比べて何がすごい？

+ [torchdiffeq](https://github.com/rtqichen/torchdiffeq)
    + PyTorch でソルバーを記述
    + 完全なソルバー一式が提供されていない（できない？）
+ [ROBER ODE](https://www.radford.edu/~thompson/vodef90web/problems/demosnodislin/Single/DemoRobertson/demorobertson.pdf)
    + C++パッケージ SUNDIALS の CVODE インテグレータ
    + ここで利用されている手法では、硬い微分方程式が解けない
+ [Ernst Hairer’s Fortran Suite](https://www.unige.ch/~hairer/software.html) の `dopri`
    + 硬い微分方程式が解けない（↑と同様）
+ [DiffEqFlux.jl](https://github.com/JuliaDiffEq/DiffEqFlux.jl)
    + MLパッケージ（＝[Flux.jl](https://github.com/FluxML/Flux.jl/)）固有の実装ではなく [DifferentialEquations.jl](https://github.com/JuliaDiffEq/DifferentialEquations.jl) の実装をそのまま利用・統合
    + あらゆる微分方程式モデル・ソルバーをそのまま利用可能

---

## どうやって有効だと検証した？

+ DDE/SDE のサンプルを提示。
    + [ブログ記事](https://julialang.org/blog/2019/01/fluxdiffeq) 参照

---

## 議論はある？

+ 特になし

---

## 次に読むべき論文は？

+ [Neural Ordinary Differential Equations](https://arxiv.org/abs/1806.07366)
+ [Reinforcement Learning vs. Differentiable Programminga](https://fluxml.ai/2019/03/05/dp-vs-rl.html)
    + DiffEq を利用して強化学習の古典的な問題を解く話（ブログ記事）
