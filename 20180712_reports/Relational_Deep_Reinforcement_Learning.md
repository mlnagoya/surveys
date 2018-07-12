Relational Deep Reinforcement Learning
===

2018/06/05
Vinicius Zambaldi, David Raposo, Adam Santoro, Victor Bapst, Yujia Li, Igor Babuschkin, Karl Tuyls, David Reichert, Timothy Lillicrap, Edward Lockhart, Murray Shanahan, Victoria Langston, Razvan Pascanu, Matthew Botvinick, Oriol Vinyals, Peter Battaglia

*DeepMind

[https://arxiv.org/pdf/1806.01830.pdf](https://arxiv.org/pdf/1806.01830.pdf)

（まとめ：@kmiwa）

---
## どんなもの？・手法
- 得られた事例同士の関係に関する表現を導入することにより、保持している事例から行動価値関数を一般化
- Sample Complexityの改善、汎化能力の向上させる

---
## 貢献
- 関係推論をベースとするBox-Worldと呼ばれるRLタスクを作成して分析
- 関係表現を創造する能力を持ったエージェントが、そうではないものと比較して、高い一般化を示した
- また、スタークラフトIIの難しい問題に対して、良いパフォーマンスを達成した


---
## どうやって有効だと検証した？
![](https://i.imgur.com/lbimY3Y.png)

- Box-World
![](https://i.imgur.com/EkuQTbU.png)
![](https://i.imgur.com/sa5a56D.png)
![](https://i.imgur.com/ZRUQkmf.png)

- StarCraft II mini-game
![](https://i.imgur.com/8kGhSMC.png)


---

## 技術や手法の肝は？
![](https://i.imgur.com/5IMQap5.png)
- Relational module という「Multi-head dot product attention」層を使ったネットワークを構築

![](https://i.imgur.com/ChOaq9C.png)

- Dot Product Attentionは、入力ベクトルであるquery、key、valueをそれぞれ、Q、K、Vとして、上式のように表現される 　


---

## 議論はある？
- より洗練された構造化知覚推論のためのコンピュータビジョンに利用できないか
- 以前からあるRelational 強化学習で、エージェントが学習したセマンティックスを深く追求できないか

---

## 次に読むべき論文は？
- [Relational recurrent neural networks](https://arxiv.org/abs/1806.01822) 
Lilicrapらによる同時期の論文



