論文のタイトル
===


# [Algorithms for Inverse Reinforcement Learning](http://www.andrewng.org/portfolio/algorithms-for-inverse-reinforcement-learning/)

Andrew Y. Ng ,
Stuart J. Russell<BR>
July 02, 2000 

## どんなもの？

- MDP(Markov Decision Process:マルコフ決定過程) における逆強化学習問題を扱う
- 動物や⼈間の学習を計算モデルとして扱い、強化学習が起きていることが証明されている。この時、報酬関数は既知で固定されていると仮定している。
- 最適な政策の報酬関数を求めることができれば、問題を解決できる。
- エキスパートの方策が最適方策となる報酬関数を推定する。

## どうやって有効だと検証した？

- Grid World で最適方策と真の報酬関数を決め、線形関数近似で推定した最適報酬関数が真の報酬関数に近いことを確認した
- Mountain Car  問題で、26のガウス関数の組み合わせを真の報酬関数とするて、最適な報酬関数を推定できた
- 状態が [0,1] X [0,1] の平面を　５X5のrGrid World で表現する問題を考えた時、2次元ガウス関数の 15 X 15 配列の全ての線形結合で真の報酬を近似した時、最適な報酬関数が推定できた


## 技術や手法の肝は？

- **強化学習** は報酬 $r$ をもとに計算される状態価値関数 $V^π$ or 行動価値関数 $Q^π$ を最⼤にするような最適⽅策$π^*$を⾒つける
- **逆強化学習** は最適な⽅策 $π$によって⽣成される系列に基づいて、最適な報酬関数を推定すること
    
- 定理
 - 定理1 : ベルマン方程式
 - 定理2 : ベルマン最適性
 - 定理3 : 有限状態空間のベクトル不等式

- アルゴリズム１
 - LP(線形計画法)定式化とペナルティー項
 
- アルゴリズム２
 - 大規模な状態空間での線形関数近似

- アルゴリズム３
 - アルゴリズム１、２では遷移確立などのモデルが必要
 - サンプル系列から報酬関数を推定する
  - 最適方策πのもとでm-モンテカルロでサンプル生成
  - i=1,2,....d で基底関数 Vi を定義
  - パラメータ α1,α2,....αd を求める


## 議論はある？

- 中程度の連続環境でも離散環境でも有効なことが分かった。
- 次の問題が残っている。
 - より簡潔な報酬機能を回復するIRLアルゴリズムを設計する
 - 実際に観測され、ノイズが入っているデータでも最適化できる指標は何か
 - 行動と最適性が強く矛盾しているとき、状態空間の特定部分に対して部分的な報酬関数を特定する
 - 報酬関数の識別可能性を最大にするには、どのような試みがあるか
 - 部分的観測可能な環境に、提案したアルゴリズムがどの程度うまく適合するか


## 先行研究と比べて何がすごい？

- その後の逆強化学習の研究への影響を考えると、重要である。


## 次に読むべき論文は？

- [Apprenticeship Learning via Inverse Reinforcement Learning](https://arxiv.org/abs/1206.5264)
- [Feature Construction for Inverse Reinforcement Learning](https://homes.cs.washington.edu/~zoran/firl.pdf)
- [BNP-FIR Bayesian Nonparametric Feature Construction for Inverse Reinforcement Learning](https://www.ijcai.org/Proceedings/13/Papers/194.pdf)
- [Maximum Entropy Deep Inverse Reinforcement Learning](https://arxiv.org/abs/1507.04888)
- [Guided Cost Learning Deep Inverse Optimal Control via Policy Optimization](https://arxiv.org/abs/1603.00448)
- [Unsupervised Perceptual Rewards for Imitation Learning](https://arxiv.org/abs/1612.06699)
- [Time-Contrastive Networks Self-Supervised Learning from Video](https://sermanet.github.io/tcn/)
- [LEARNING ROBUST REWARDS WITH ADVERSARIAL INVERSE REINFORCEMENT LEARNING](https://arxiv.org/abs/1710.11248)
- [State Aware Imitation Learning](https://papers.nips.cc/paper/6884-state-aware-imitation-learning)

