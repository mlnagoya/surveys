Deep Learning: Exploring High Level APIs of Knet.jl and Flux.jl in comparison to Tensorflow-Keras
===

2019/06/20 Al-Ahmadgaid B. Asaad

[Blog Post](https://estadistika.github.io//julia/python/packages/knet/flux/tensorflow/machine-learning/deep-learning/2019/06/20/Deep-Learning-Exploring-High-Level-APIs-of-Knet.jl-and-Flux.jl-in-comparison-to-Tensorflow-Keras.html)

（まとめ：[@antimon2](https://github.com/antimon2)）

---

## どんなもの？

+ 数値計算に傾倒している [Julia](https://julialang.org) の DeepLearning ライブラリを調査し、TF-Keras と比較してみた
+ 結論:
    + Julia は十分に投資する価値がある
    + Julia は `for` ループ速い
    + Knet.jl は Julia + littleelse（ナットとボルト）
    + Flux.jl は入門・移行向けであり柔軟性を兼備

---

## どうやって有効だと検証した？

+ [Flux.jl](https://github.com/FluxML/Flux.jl), [Knet.jl](https://github.com/denizyuret/Knet.jl) と TF-Keras で使用方法・学習速度・学習曲線を比較
+ データセットは [Iris](https://en.wikipedia.org/wiki/Iris_flower_data_set) を使用
+ その他、Python と Julia で同条件となるようコーディング

---

## 技術や手法の肝は？

### データセットの準備

+ TF-Keras: 教師トラベルのデータを 訓練用 と 検証用 に分ければ準備終わり
    + ミニバッチ分割・データ流し込みは自動
+ Knet.jl: （分割した）データから `minibatch` オブジェクトを生成し訓練に利用
+ Flux.jl: ラベルデータに one-hot エンコーディングが必要
    + バッチ生成等は独自実装できる柔軟性を残している

### モデル構築

+ 3層MLP
    + TF-Keras, Knet.jl, Flux.jl ともに実装方法については大差はなし
+ 内部実装
    + TF-Keras: 53% は C++実装
    + Knet.jl/Flux.jl: いずれも 100% Julia

### 訓練

+ TF-Keras: `model.compile()` → `model.fit()`
    + `.fit()` で訓練データ・検証データ・バッチサイズ・エポック数を指定
+ Knet.jl: `adam!(model, repeat(dtrn, 100))`
    + 検証を含むには `for x in adam(model, repeat(dtrn, 100)) ～` のようにしてループ内で処理
+ Flux.jl: `Flux.@epochs 100 Flux.train!(loss, Flux.params(model), minibatches, Flux.ADAM(), cb=callback)`
    + `callback` に無引数関数を指定、検証やログ出力はその中で実行（もしくは `for` ループにしてその中で）

![Loss比較](https://i.imgur.com/a55jxh6.png)

### 評価

![Accuracy比較](https://i.imgur.com/889wASU.png)

### ベンチマーク

![ベンチマーク](https://i.imgur.com/1EEdtbt.png)

---

## 議論はある？

+ コードが全体的に不公平
    + TFは内部で毎エポックシャッフルが走る（はず）だが、Julia側のコードは単純なデータ分割＋シャッフル最初の1回だけの模様
    + よく見るとそれぞれでバッチサイズ合ってない、1エポック辺りの事例数も合ってない
    + 100エポックとは言え Iris データセット（事例数合計150、入力4次元出力3次元）なので性能検査するには小さすぎる
    + ⇒Julia側の各結果は「バッチ（再）生成時間が含まれていないために速かった」「データが偏っていたためにたまたま精度が良かった」可能性が高い

### 独自再検証

+ （別件のデモのために）[Fashion-MNIST](https://github.com/zalandoresearch/fashion-mnist) で（主に速度を）再検証
    + 速度重視、精度軽視（バッチ生成手抜き、バッチサイズと1エポック辺りの事例数は同等になるよう処理）
    + 結果 → [Knet.jl](https://nbviewer.jupyter.org/gist/antimon2/2939e75f2620112ac0525c677beab41c/FashionMNIST_Knet_Sample.jl.ipynb) / [Flux.jl](https://nbviewer.jupyter.org/gist/antimon2/2939e75f2620112ac0525c677beab41c/FashionMNIST_Flux_Sample.jl.ipynb) / [TF-Keras](https://nbviewer.jupyter.org/gist/antimon2/2939e75f2620112ac0525c677beab41c/FashionMNIST_TfKeras_Sample.py.ipynb)
+ CNN（Conv層）を含めた学習は TF-Keras が圧倒的に速い
    + GPU不使用、CPU上の Conv の実装の問題かもしれない

---

## 先行研究と比べて何がすごい？

+ 《特になし》

---

## 次に読むべき ~~論文~~ 記事は？

+ 「GPUを利用したモデル訓練に今後取り組みたい」と言っているので、その記事が上がったらそれ。
