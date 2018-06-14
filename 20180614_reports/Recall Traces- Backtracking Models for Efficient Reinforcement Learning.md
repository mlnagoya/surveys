Recall Traces: Backtracking Models for Efficient Reinforcement Learning
===

2018/04/02  
Anirudh Goyal *1
Philemon Brakel *2 
William Fedus *1 
Timothy Lillicrap *2 
Sergey Levine *3 
Hugo Larochelle *4
Yoshua Bengio *1

1 MILA, University of Montreal 
2 Google Deepmind 
3 University of California, Berkeley 
4 Google Brain

[https://arxiv.org/pdf/1804.00379.pdf](https://arxiv.org/pdf/1804.00379.pdf)   
[https://www.youtube.com/watch?v=vSVRVuRTYB8](https://www.youtube.com/watch?v=vSVRVuRTYB8)

（まとめ：@kmiwa）

---
## どんなもの？・手法
- 強化学習において高い報酬が得られる状態は少なく，これを優先的に学習する
- 価値の高い状態からそこに到る（状態、行動）対（これをRecall Tracesと呼ぶ）を予測し、学習の改善・パフォーマンスの向上を実現した


---
## 貢献
- backtracking modelを使って、sample complexity　を改善しより早い学習が行えることを実証した


---
## どうやって有効だと検証した？
### 以下のシチュエーションによる実験を行い、学習の高速化と高い報酬が確認できた
- Access to True Backtracking Model
- Learned Backtracking Model from Generated States
- Learned Backtracking Model - On-Policy Case
- Learned Backtracking Model - Off-Policy Case


---

## 技術や手法の肝は？
### Backtracking Model
- φによってパラメーター化された一つ前の(s,a)のタプルによる同時確率分布の密度推定

### 価値の高い状態を作る（２つのメソッドを利用）
- 最も価値の高い状態であるバッファβの値を利用する
- Goal GAN(*GANを利用してゴールである状態gを生成する方法)を利用する

### Backtracking Modelを使ったポリシーの改善
#### Training Backtracking Model
- use a maximum likelihood training loss for training of the backtracking model Bφ on the top k% of the agent’s trajectories stored in the state buffer β
- agent trajectories t に対して確率的確勾配降下法を利用
![](https://i.imgur.com/lAgNYrs.png)
#### Improving the Plocy from the Recall Traces
- backtracking model　によって生成される　traces 〒 をエージェントによるimitation learning（模倣学習）の観測として使用する
![](https://i.imgur.com/YxYPMjV.png)
![](https://i.imgur.com/Zvzgupd.png)

---

## 議論は？
- 従来のモデルベースシステムから、フォワードモデルと組み合わせてbacktrackingモデルを利用できるようにする

---

## 次に読むべき論文は？
- Goal GAN(Automatic Goal Generation for Reinforcement Learning Agents)
  [https://arxiv.org/pdf/1705.06366.pdf](https://arxiv.org/pdf/1705.06366.pdf)
