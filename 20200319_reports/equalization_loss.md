Equalization Loss for Long-Tailed Object Recognition
===

Jingru Tan, Changbao Wang, Buyu Li, Quanquan Li, Wanli Ouyang, Changqing Yin, Junjie Yan

https://arxiv.org/abs/2003.05176

@cohama


## どんなもの?

- Long Tail (物体のクラスの偏りが大きい) 問題に対して新しい損失関数を考えた
  - `L = Σj wi log(pj)`
  - `wj = 1 - E(r) T(fj) (1 - yj)`
    - `E(r)` は画像 r が背景かどうか
    - `T(fj)` はクラス `j` の頻度 `fj` があるしきい値 `λ` 以下かどうか
      - `λ` は 1.76e-4 くらいが良いらしい (LVIS の場合だと思われる)
    - つまり、`w` は
      - 背景である、かつ、頻度の低いクラス、かつ、正解が `j` でないときときに Loss が 0 になる
- Focal Loss や Class Balanced Loss などと比較しても強い
- 分類問題でも使える
  - E(r) の代わりにベルヌーイ分布を使う

## 先行研究と比べて何がすごい？

- Focal Loss はサンプルレベルでの偏りを調整
- Class で重みを付けるやつはクラスレベルで偏りを調整
- Equalization Loss はクラスレベルとサンプルレベルを同時に対策できる

## どうやって有効だと検証した？

- LVIS というクラスの偏りが大きい物体検出のデータセットで1位

## 議論はある?

- Single Shot に応用したい場合はどうすれば良さそうか？

## 次に読むべき論文
- Class-aware Sampling
- Repeat Factor Sampling
- Class-balanced Loss
- Focal Loss
