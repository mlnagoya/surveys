One Billion Word Benchmark for Measuring Progress in Statistical Language Modeling
===

2013/12/11 Ciprian Chelba, Tomas Mikolov, Mike Schuster, Qi Ge, Thorsten Brants, Phillipp Koehn, Tony Robinson (Google)

[https://arxiv.org/abs/1312.3005](https://arxiv.org/abs/1312.3005)

（まとめ：@nharu1san）

---

## どんなもの？
+ 10億語を利用して言語モデル評価用のデータセットを作成した

---

## 先行研究と比べて何がすごい？
+ 10億語を使用することにより妥当性がある上、Web上で公開するため容易に利用可能
  + [https://github.com/ciprian-chelba/1-billion-word-language-modeling-benchmark](https://github.com/ciprian-chelba/1-billion-word-language-modeling-benchmark)
+ 大規模なRNNでベースラインに比べてパフォーマンスの向上が確認できた

---

## 技術や手法の肝は？
+ [WMT11](http://statmt.org/wmt11/)にて配布されているテキストデータをベースに作成

---

## どうやって有効だと検証した？
![表1](https://i.imgur.com/QXKxEyX.jpg)
+ ベースラインとしてKatzらのモデル(1995)およびKneserとNeyのモデル(1995)を5-gramで使用、RNN等と比較を行った

---

## 議論はある？
+ Discussion節無し

---

## 次に読むべき論文は？
+ [Dissecting Contextual Word Embeddings: Architecture and Representation](https://arxiv.org/abs/1808.08949)
