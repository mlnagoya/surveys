Continuous Deep Q-Learning with Model-based Acceleration
===

2016/03/02  
Shixiang Gu *1 *2 *3  
Timothy Lillicrap *4  
Ilya Sutskever *3 
Sergey Levine *3  
*1 University of Cambridge  *2 Max Planck Institute for Intelligent Systems  *3 Google Brain   *4Google DeepMind

[https://arxiv.org/abs/1603.00748](https://arxiv.org/abs/1603.00748)

（まとめ：@kmiwa）

---
## どんなもの？・手法
- 連続領域においてモデルベースを活用したDeep Q-Learnig
- NAF(Normalized Advantage Functions)により、DQNを連続領域で利用できるようにする
- 次にモデルフリー強化学習を向上させるために、モデルベースを利用

---
## 貢献
- 連続領域において、効果的なQ-Learningを可能とするQ関数の表現を導入し評価した
- 学習済みのモデルをモデルフリーQ-Learningに組み込むため、いくつかの選択肢を評価し、連続性制御タスクで効果があった
- 局所線形モデルと局所on-policy（学習の過程で方策の評価、改善が行われるもの）のimagination rolloutsを組み合わせることで、モデルフリーの連続性Q-Learningを向上させ、sample complexity(対象とするデータがスパースに表現されるための基底 を一意に同定するために必要なサンプル数)の大きな向上があった

---
## どうやって有効だと検証した？
- シュミレーションによる幅広いロボットタスクに対して、上記手法を適用し、従来方法と比較
- ほとんどの実験で従来手法より、より早く（最大従来手法の18.8%程度で）、より高い報酬となった。
---

## 技術や手法の肝は？
### 前提
- NAF:領域が連続、Q-Learning
- DQN: 領域が離散、Q-Learning
- DDPG: 領域が連続、Actor Critic

### NAF
- Q-Learning更新時に、簡単にかつ解析的に最大値（arm gax）を取得できるQ-LearningにおけるQ関数を表現。
- 関数V（valuve function terv V(x)）と関数A（advanteg term A(x,u)）をそれぞれ計算し、非線形の２次関数で表現する

#### With Model-Based Acceleration
- 特定のタイプのモベルベースQ-LearningとNAFを結合させる
- ロボティクスや自動運転での利用を行えるように　imagination rollouts　を利用する


---

## 議論はある？
- モデルとなるアルゴリズムを注意深く選ぶ必要がある
- トレーニングニューラルネットワークモデルでは、実質的な改善が見られなかった 

---

## 先行研究と比べて何がすごい？
- モデルフリーのディープ強化学習において、サンプルの利用の大幅な有効活用
- DDPG（Actor Critic）よりもシンプル

---

## 次に読むべき論文は？
- [Recall Traces: Backtracking Models for Efficient Reinforcement Learning](https://arxiv.org/abs/1804.00379)
  - Lillicrapらのより新しい論文

