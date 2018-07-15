[Simple random search provides a competitive approachto reinforcement learning](https://arxiv.org/pdf/1803.07055.pdf)
===

[サンプルコード](https://github.com/modestyachts/ARS)


## どんなもの？

- パラメータに摂動を導入した[進化戦略](https://arxiv.org/abs/1703.03864)を発展させて、深層学習を使わず大規模な並列処理で高速化とロバストな強化学習を提案している。


## どうやって有効だと検証した？

- OpenAI Gym Mujoco で　Swimmer-v1,Hopper-v1,HalfCheetah-v1,Walker2d-v1,Ant-v1,Humanoid-v1　について　ARS(今回提案手法 : Augmented Random Search), TRPO, NG-1, NG-2 のアルゴリズムについて　報酬がしきい値に達するまでのエピソード数を比較。
<img src="https://github.com/shuuichi/surveys/blob/master/20180614_reports/ARS03.png" alt="写真" width="600"> 

- ARS,PPO,A2C,CEM,TRPO のアルゴリズム毎に　Swimmer-v1,Hopper-v1,HalfCheetah-v1,Walker2d-v1　で　最大平均報酬を比較。
<img src="https://github.com/shuuichi/surveys/blob/master/20180614_reports/ARS04.png" alt="写真" width="600"> 

- MuJoCoの移動作業におけるARSとESおよびTRPOの方法で、報酬閾値に達するのに必要な平均タイムスペップ数を比較。
<img src="https://github.com/shuuichi/surveys/blob/master/20180614_reports/ARS05.png" alt="写真" width="600"> 

- Humanoid-v1タスクの平均報酬6000に達するのに必要な時間の評価(進化戦略に比べて約15倍速くなった)
<img src="https://github.com/shuuichi/surveys/blob/master/20180614_reports/ARS06.png" alt="写真" width="600"> 

- Humanoid-v1タスクで平均報酬が6000に達するのに必要な時間を比較。
<img src="https://github.com/shuuichi/surveys/blob/master/20180614_reports/ARS07.png" alt="写真" width="600"> 

## 技術や手法の肝は？
- 摂動をr利用した基本的なランダム探索(1965 Random optimization: Automation and Remote control)
<img src="https://github.com/shuuichi/surveys/blob/master/20180614_reports/ARS01.png" alt="写真" width="600"> 

- 今回提案のアルゴリズム
<img src="https://github.com/shuuichi/surveys/blob/master/20180614_reports/ARS02.png" alt="写真" width="600">

- 今回提案のアルゴリズム
  - V1 : 報酬の標準偏差によるスケーリング
  - V2 : 状態の正規化
  - V1-t,V2-t : 大きいほうの報酬を使う : 摂動の報酬の大きいほうの報酬の上位b個の報酬で重みを計算する

- 並列化に使用したライブラリー
  -  [Python  library  Ray ](https://github.com/ray-project/ray)

## UdemyでARSの講座が安くなっていたので受けてみた

- Mujoco の代替えのフリーな物理エンジンを使った。(OpenAI Gym サポートしてます)
  - [pybullet](https://pypi.org/project/pybullet/) - pip install pybullet

- Halfcheetaを実装してみた結果
  - 並列処理でなく１CPUで学習したのでCorei7で7時間くらいかかった。
  - [ARS Halfcheeta-1](https://youtu.be/VS8ovl9ntyE)
  - [ARS Halfcheeta-2](https://youtu.be/JLZvPm43SMg)
  - [ARS Halfcheeta-3](https://youtu.be/d9oKOJOntgI)

## 今回確認できなかったこと

- Observation Space と Action Space が決まればモデルフリーな強化学習ができることは分かったが、

- OpenAI Gym CartPole-v0 をARSで学習させてみたい。(BOX Discrete について調べて時間切れになった)

## 先行研究と比べて何がすごい？

- 深層学習を使わないで強化学習ができること。

## 次に読むべき論文は？

- より複雑な問題を解決する考えがあると書いてあるので、次の論文が出たら読んでみたい。
- [Apprenticeship Learning via Inverse Reinforcement Learning](https://arxiv.org/abs/1206.5264)
- [Feature Construction for Inverse Reinforcement Learning](https://homes.cs.washington.edu/~zoran/firl.pdf)
- [BNP-FIR Bayesian Nonparametric Feature Construction for Inverse Reinforcement Learning](https://www.ijcai.org/Proceedings/13/Papers/194.pdf)
- [Maximum Entropy Deep Inverse Reinforcement Learning](https://arxiv.org/abs/1507.04888)
- [Guided Cost Learning Deep Inverse Optimal Control via Policy Optimization](https://arxiv.org/abs/1603.00448)
- [Unsupervised Perceptual Rewards for Imitation Learning](https://arxiv.org/abs/1612.06699)
- [Time-Contrastive Networks Self-Supervised Learning from Video](https://sermanet.github.io/tcn/)
- [LEARNING ROBUST REWARDS WITH ADVERSARIAL INVERSE REINFORCEMENT LEARNING](https://arxiv.org/abs/1710.11248)
- [State Aware Imitation Learning](https://papers.nips.cc/paper/6884-state-aware-imitation-learning)

