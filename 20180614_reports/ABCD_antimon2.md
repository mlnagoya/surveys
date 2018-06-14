Input and Weight Space Smoothing for Semi-supervised Learning
===

2018/05/23 Safa Cicek, Stefano Soatto (University of California)

https://arxiv.org/abs/1805.09302

（まとめ：[@antimon2](https://github.com/antimon2)）

---

## どんなもの？

+ 入力と重みの両方を平滑化する正則化
+ 簡単な仕組みで、大幅な Data Augmentation に頼ることなく最先端の性能を実現

---

## 技術や手法の肝は？

+ ABCD アルゴリズム
    + ABCD = Adversarial Block Coordinate Descent（ABCD）
    + 勾配上昇と勾配下降の組合せ（η<sub>A</sub> ≪ η<sub>D</sub>）
+ 最小化：
    + エントロピーをABCDで（重み平滑化）
    + VATをSGDで（入力平滑化）

---

## どうやって有効だと検証した？

+ ABCD と SGD で堅牢性を比較
+ CIFAR-10 と SVHN データセットでテスト誤差を比較

---

## 先行研究と比べて何がすごい？

+ 勾配にランダムノイズを加えて正則化を図る過去の研究がある
    + ABCDは「敵対的なノイズ」を加えている

---

## 議論はある？

+ 入力平滑化：グラフベースの手法が存在する
+ 重み平滑化：教師-生徒モデル

---

## 次に読むべき論文は？

+ [Virtual Adversarial Training: a Regularization Method for Supervised and Semi-supervised Learning](https://arxiv.org/abs/1704.03976)
    + この論文でも利用しているVATの研究
+ [Adversarial Dropout for Supervised and Semi-supervised Learning](https://arxiv.org/abs/1707.03631)
    + 同じく半教師あり学習で、VATとVAdDを組み合わせた研究

