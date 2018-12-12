Partial Convolution based Padding
===

2017/10/27 Guilin Liu, Kevin J. Shih, Ting-Chun Wang, Fitsum A. Reda (NVIDIA)

https://arxiv.org/abs/1811.11718

（まとめ：[@antimon2](https://github.com/antimon2)）

---

## どんなもの？

+ 部分畳み込みを利用した新しいパディング手法
    + ゼロ埋め、反射、複製に代わるモノ

---

## 先行研究と比べて何がすごい？

+ ゼロ埋めは画像分類等で悪影響大きい
+ 反射・複製パディングもImageNetで問題あることを検証
+ 提案手法で学習すれば他のパディングでの推論にも使える

---

## どうやって有効だと検証した？

+ 画像分類タスクで、精度と収束性を比較
+ セグメンテーションタスクで特に境界付近の性能を比較

---

## 技術や手法の肝は？

+ 部分畳み込み（Partial Convolution）
    + 元々は穴あき画像のような不完全な入力データを扱うための提案されたもの
    + ↑を利用し、パッディング領域を穴とみなして係数を計算して畳み込みを行う↓  
    ![Fig2](https://i.imgur.com/wvQASi0.png)  
    ![Eq4,Eq5](https://i.imgur.com/HNITA36.png)

---

## 議論はある？

+ 特になし

---

## 次に読むべき論文は？

+ [Image Inpainting for Irregular Holes Using Partial Convolutions](https://arxiv.org/abs/1804.07723)
    + 部分畳み込みを利用した穴あき画像の補間
    + ↑この論文のパディングの根幹部分
