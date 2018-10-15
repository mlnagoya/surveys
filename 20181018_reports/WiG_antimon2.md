Weighted Sigmoid Gate Unit for an Activation Function of Deep Neural Network
===

2018/10/03 Masayuki Tanaka (産業技術総合研究所)

https://arxiv.org/abs/1810.01829

（まとめ：[@antimon2](https://github.com/antimon2)）

---

## どんなもの？

+ WiG（Weighted Sigmoid Gate unit）の提案
    + ReLUやSwishの一般化
    + Vectorに対する活性化関数

---

## 技術や手法の肝は？

![WiGunit.jpg](https://i.imgur.com/cdYEo84.jpg)

+ <code>f(x) = x ⊙ σ(W<sub>g</sub>x + b<sub>g</sub>)</code>
    + `x` は入力（N次元ベクトル）
    + <code>W<sub>g</sub></code>はN×N行列、<code>b<sub>g</sub></code>はN次元ベクトル（訓練パラメータ）
    + `σ` は sigmoid 関数、`⊙` は要素ごとの積
+ 重み付きの入力に対するバージョン、畳み込み層に適用するバージョン等あり

---

## 先行研究と比べて何がすごい？

+ <code>b<sub>g</sub> = <b>0</b></code>、<code>W<sub>g</sub> = I</code>（単位行列）でSiL（Swish）と同じ
    + <code>W<sub>g</sub> = sI (s ≫ 1)</code> なら ReLU に近似
+ <code>W<sub>g</sub> = sI</code> <code>b<sub>g</sub> = <b>0</b></code> で初期化して訓練する
+ L1正則化

---

## どうやって有効だと検証した？

+ ReLU 初め他のいくつかの活性化関数と比較実験
+ CIFAR-10/100で
    + 訓練時のloss推移比較
    + 検証精度（正解率）比較
+ ノイズ除去タスクで精度（PSNR/SSIM）比較

---

## 議論はある？

+ 論文中には特にないが…
    + 学習時間・推論時間への影響は？
    + WiGを利用したネットワークの転移学習は？

---

## 次に読むべき論文は？

+ [Searching for activation functions](https://arxiv.org/abs/1710.05941)
    + Swish の紹介と、効果的な活性化関数を探す話
    + 以前読んだ→ https://github.com/mlnagoya/surveys/blob/master/20180412_reports/Swish_antimon2.md
