# Using Grouped Linear Prediction and Accelerated Reinforcement Learning for Online Content Caching

## https://arxiv.org/pdf/1803.04675.pdf


### どんなもの？

* スマホ通信において、キャッシュを効率的に使うための手法
  - GLM（Grouped Linear Model）は、キャッシュするコンテンツの予測
  - RLMA(reinforcement learning approach with model-free acceleration)は、コンテンツの入れ替えコストの削減

  
### どうやって有効だと検証した

- MovieLens(https://movielens.org)を使った検証

- GLM
   - LRU(Least Recently Used)、LFUDA(Least Frequently Used with Dynamic Aging)との比較

    - LFUDAよりも15.2%、LRUよりも170.6%向上

- RLMS
  - LFUDA, Origin QL, Most Popular(by GLM), LRU　に比べて、　15.6%, 22.6%, 28.8%, 30.8% の向上

  
### 技術や手法の肝は？

- GLM

  - コンテンツのageによりグループ化して、過去の情報を含んだ学習を行う

- RLMS

  - GLMにより算出された予測値を使うことで、複雑で変化の激しい環境での強化学習を行う

  
### 議論はある？

- 複数ノードでの実証

  
### 先行研究と比べて何がすごい？

- GLMの場合

  - 一般的に利用されるIRM(IRM　conceptual model used in the analysis of storage system: disk drives, caches, etc.）は、過去の情報からも紐付できない

  - 最近利用されるようになったSNM(Shot Noise Model)は、IRMより過去データとの相関関係を構築できるが、,コンテンツリクエストが指数関数的減衰になるため実用的でない

  - 上記を解決し、パフォーマンスの向上する

- RLMSの場合

  - ネットユーザーの嗜好、新しいコンテンツが常に出てくるため、リクエスト情報は非常に変化する。このような状況では、確率的近似値は最適なQ値に収束しない

  - 学習するためのサンプルも不十分で、固定の学習率でもQ値が定まるとは言えない

  - 上記を解決し、パフォーマンスの向上する

  
### 次に読むべき論文は？

- Continuous Deep Q-Learning with Model-based Acceleration https://arxiv.org/abs/1603.00748

- Using early view patterns to predict the popularity of youtube videos https://dl.acm.org/citation.cfm?id=2433443


