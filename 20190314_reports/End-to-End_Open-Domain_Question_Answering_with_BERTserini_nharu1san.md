End-to-End Open-Domain Question Answering with BERTserini
===

2019/02/05 Wei Yang, Yuqing Xie, Aileen Lin, Xingyu Li, Luchen Tan, Kun Xiong, Ming Li, Jimmy Lin
[https://arxiv.org/abs/1902.01718](https://arxiv.org/abs/1902.01718)

（まとめ：@nharu1san）

---

## どんなもの？
[Anserini](https://github.com/castorini/Anserini)という検索エンジンとBERTを組み合わせてオープンドメインな質問に回答できるようにした
![図1](https://i.imgur.com/IZugYGm.png)

---

## 先行研究と比べて何がすごい？
- オープンドメインなところ
- Anserini+BERTなところ

---

## どうやって有効だと検証した？
SQuAD(v1.1)で他手法と比較
![表1](https://imgur.com/wPJrl4g.png)

---

## 技術や手法の肝は？
![図2](https://i.imgur.com/9HRW44W.png)
![図3](https://imgur.com/5CdWaHk.png)
Anseriniで関係する文章をインデックス済みのWikipediaデータから抽出し, BERT(SQuADで学習済み)とAnseriniのスコアで回答を決定する

---

## 議論はある？
- Discussion節なし

---

## 次に読むべき論文は？
- [Reading Wikipedia to Answer Open-Domain Questions](https://arxiv.org/abs/1704.00051)
  - DrQAについて
- [R^3: Reinforced Reader-Ranker for Open-Domain Question Answering](https://arxiv.org/abs/1709.00023)
  - R^3について