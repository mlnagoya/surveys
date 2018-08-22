# State Abstractions for Lifelong Reinforcement Learning

- author: David Abel, Dilip Arumugam, Lucas Lehnert, Michael Littman
- publication: ICML2018 ([PMLR 80:10-19, 2018](http://proceedings.mlr.press/v80/abel18a.html))


----


## どんなもの？

- *State Abstraction* と呼ばれる技術を用いたLifelong強化学習に対する理論的な貢献
  - *Abstraction* は状態空間を抽象化/圧縮することでサンプル効率性を向上させる技法の1つ
  - 理論的な貢献: 理論的な議論を行うために新しいクラス×2を提案
  - 実験的な貢献: 数値実験からサンプル効率が高い強化学習を実現し、Abstractionの良い点と悪い点を示した

- Lifelong強化学習について
  - 状態集合$S$と行動集合$A$は共通
  - 遷移モデル$T$と報酬モデル$R$がある分布$D$から継続的に与えられる

![fig1](https://i.imgur.com/458KPBw.png)


## 先行研究と比べてどこがすごい？

- 抽象化関数$\phi$の評価基準には「損失」と「Transitive」を用いる場合、本研究の貢献は「Transitive」な$\phi$であり、かつ誤差が小さい抽象化が達成されていること
- *State Abstraction* 一覧表と提案手法の表が参考になる

![table1](https://i.imgur.com/yZ6v9Pi.png)


## 技術や手法の肝は？

- 抽象化の意味: 状態s1と状態s2について、述語$\phi(s1,s2)$が真であれば、同一の状態と見なす
- 「Transitive」（推移的）という特徴を入れたクラスを定式化して理論をゴリゴリやったこと
- 「Transitive」とはs1とs2が真で、s2とs3が真であるとき、s1とs3も真になるような関係

## どうやって有効だと検証した？

- すでに証明されているクラスのサブクラスであるため、既存の理論的な損失バウンドが利用できる
- 実験的には抽象化ありとなしの場合で、Q学習と価値反復法を利用したLifelong強化学習に適用して累積報酬を見た
- 一例

![fig3](https://i.imgur.com/8J4Zdj8.png)

## 議論はある？

- 関数$\phi$が天下り的に与えられること（著者の発表でもこれを学習できたら最高みたいなことを言っていた）
- $S$だけではなく$A$も抽象化できるとサブタスクっぽい感じになるかもしれない
- 理論的な研究なので実験実証が簡単なドメインのみ

## 次に読むべき論文は？

- 理論的には先端を行っているので、著者のgithubを眺めてみるのが良い: https://github.com/david-abel/rl_abstraction
