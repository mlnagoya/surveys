DocBERT: BERT for Document Classification
===

2019/04/17 Ashutosh Adhikari, Achyudh Ram, Raphael Tang, Jimmy Lin(David R. Cheriton School of Computer Science University of Waterloo)
[https://arxiv.org/abs/arxiv_1904.08398](https://arxiv.org/abs/arxiv_1904.08398)

（まとめ：@nharu1san）

---

## どんなもの？
- BERTでドキュメント分類を行った

---

## 先行研究と比べて何がすごい？
- 検証した4つのデータセットでstate of the art

![表2](./arxiv_1904.08398/table2.png)

---

## どうやって有効だと検証した？
- Reutar, AAPD, IMDB, Yelp 2014の4つのデータセットでSVMやLSTM, CNNを用いた手法(HAN, KimCNN, XMLCNN, SGM)と比較した

![表1](./arxiv_1904.08398/table1.png)

---

## 技術や手法の肝は？
- BERTのSingle Sentenceと同様にoutput layer付きのモデルを用いてドキュメント分類を行った

![図1](./arxiv_1904.08398/figure1.png)

---

## 議論はある？

---

## 次に読むべき論文は？
