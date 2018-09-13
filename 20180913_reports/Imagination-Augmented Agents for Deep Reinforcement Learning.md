Imagination-Augmented Agents for Deep Reinforcement Learning
===

2016/06/19 
Théophane Weber, Sébastien Racanière, David P. Reichert, Lars Buesing, Arthur Guez, Danilo Jimenez Rezende, Adria Puigdomènech Badia, Oriol Vinyals, Nicolas Heess, Yujia Li, Razvan Pascanu, Peter Battaglia, Demis Hassabis, David Silver, Daan Wierstra

[https://arxiv.org/pdf/1707.06203](https://arxiv.org/pdf/1707.06203)

（まとめ：@kmiwa）

---
## どんなもの？・手法
- Deep 強化学習にて、モデルを正確に測定するのは難しい
- 代わりに不正確なプランニングメソッドから使える情報を活用する
- 抽出は、ニューラルネットワークに渡して行う
- プランニングメソッドだけでは、行動を決定できないので、モデルフリーメソッドのRLも学習して活用する

---
## 貢献
- 不正確なプランニングをニューラルネットワークで処理する事で、モデルフリーメソッドに取り込めた

---
## どうやって有効だと検証した？
### 倉庫番（ゲーム）
![](https://i.imgur.com/nAJOM5C.png)
![](https://i.imgur.com/wuRQe6M.png)
![](https://i.imgur.com/BntN7KE.png)
- ブロックを特定の位置まで運ぶゲーム
- プランニングメソッドが求められる特性を持つ
- I2Aがstandardを上回る
- poor model(パラメーターを落として精度を下げたモデル)でもタスク成功率が落ちない

---

### ミニパックマン
![](https://i.imgur.com/qS9HjjZ.png)
- 一つのモデルで異なるタスクに使える内部モデルを学習できるか実験
- I2Aがbaselineを上回る




---

## 技術や手法の肝は？
### モデル
![](https://i.imgur.com/fFJGrQF.png)
1. コア
2. 1がプランニングに、2がそれを解釈する部分に相当
3. プランニングとモデルを結合する
### 学習
1. pre-trainをする
2. 一般的なRL
3. 一般的なRL
### imagination rollout strategy
* 選択可能な各行動から１回ずつrolloutする


---

## 議論はある？
- 他のドメインで活用できるか

---

## 先行研究と比べて何がすごい？
- model-bath pathは有効で不完全なモデルも扱える
- MCTSより読みの効率よく、タスク間汎化も可能

---

## 次に読むべき論文は？
[Relational recurrent neural networks](https://arxiv.org/abs/1806.01822)
- 




