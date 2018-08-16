Glow: Generative Flow with Invertible 1×1 Convolutions
===

2018/07/10 Diederik P. Kingma, Prafulla Dhariwal (Open AI)

https://arxiv.org/abs/1807.03039

（まとめ：[@antimon2](https://github.com/antimon2)）

---

## どんなもの？

+ Glow の提案
    + 1x1 可逆 Convolurions を利用した生成的Flow
    + 高解像度の自然画像を効率的に合成することができる文字通り最初の尤度ベースのモデル（らしい）

---

## 先行研究と比べて何がすごい？

+ Autoregressive モデル
    + 単純だが並列化不可能
+ GAN
    + 潜在性を推論するエンコーダーが全くない
    + データ全体に対する完全なサポートがない
    + 最適化困難
    + 過学習と一般化の評価が困難
+ VAE
    + 訓練・合成ともに並列化可能だが最適化に難あり
    + 潜在変数の推論が可能
+ MAF
    + 並列化できない

---

## 技術や手法の肝は？

![図2](https://i.imgur.com/sTzOxkX.png)

+ Actnorm（活性化正規化）
    + 初期バッチから与えられる平均と分散で初期化
    + スケールとバイアスはデータと独立の訓練パラメータ
    + Batch Normalization じゃない
        + ↑PUごとのバッチサイズに反比例して性能悪くなる
+ 可逆 1x1 Convolution
    + 置換演算の一般化（フィルターサイズ 1×1×c×c）
    + 重みをランダム回転行列で初期化
+ Affine カップリング層
    + チャネル方向に2分割→一方にNN適用→結合

---

## どうやって有効だと検証した？

+ 定量評価
    + 負の対数尤度（次元ごとのビット）を比較
    + 反転・ランダム置換・可逆 1x1 Convolution の3つのアーキテクチャで比較
    + Additive カップリング と Affine カップリング とで比較
    + CIFAR-10, ImageNet, LSUN の各データセットで比較
+ 定性的実験
    + 実際に画像を生成（ランダムサンプル、線形補間、意味論的操作等）

![図5](https://i.imgur.com/wY8mntd.png)


---

## 議論はある？

+ 特になし

---

## 次に読むべき論文は？

+ [NICE: Non-linear Independent Components Estimation](https://arxiv.org/abs/1410.8516)
    + 最初(?)に発表された Flow ベースの生成モデル
+ [Density estimation using Real NVP](https://arxiv.org/abs/1605.08803)
    + NICE を拡張した Flow ベースの生成モデル
