FCOS: Fully Convolutional One-Stage Object Detection
===

Zhi Tian, Chunhua Shen, Hao Chen, Tong He

[paper](https://arxiv.org/abs/1904.01355v3)

@cohama


## どんなもの?

- Anchor-Free な Single Shot Object Detection
  - Anchor-Free はアンカーの設計が不要くらいの意味
- RetinaNet と同じ構造、ハイパーパラメータで MS COCO 42.1% (+1.3)

## 技術や手法の肝は？

- 構造は RetinaNet と同じ
- 検出部分は各ピクセルから上端、左端、下端、右端までの距離を `exp(s * 入力画像の座標)` で回帰
  - s は学習させる
- さらに、centerness という値も出力させる
  - 枠の端では0、ちょうど中心で1になるような実数値
  - 2値問題 (Binary Cross Entoropy) で学習させる
  - 最後の確信度を求める際に Score と掛け算

## どうやって有効だと検証した？

- RetinaNet と同じパラメータを使って実験


## 先行研究と比べて何がすごい？

- Anchor-base な手法はパラメータ探索が大変
  - 実際 RetinaNet も最適なアンカーを探すためにたくさん実験している
- CornerNet は複雑な後処理が必要
- UnitBox、DenseBox は物体のオーバーラップをうまく扱えない


## 議論はある?

- centerness ないと弱い。
  - 中心を教えるのが単純に強い説
- Anchor Free といっているが、要は特殊なアンカーが1個あるだけでは


## 次に読むべき論文
- DenseBox https://arxiv.org/abs/1509.04874
- UnitBox https://arxiv.org/abs/1608.01471
- CornerNet https://arxiv.org/abs/1808.01244
  - 左上と右下の2点のキーポイント検出と、それらが同一物体のペアになるかを推論

- CenterNet https://arxiv.org/abs/1904.08189
