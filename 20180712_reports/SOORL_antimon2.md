Strategic Object Oriented Reinforcement Learning
===

2018/06/01 Ramtin Keramati, Jay Whang, Patrick Cho, Emma Brunskill (Stanford University)

https://arxiv.org/abs/1806.00175

（まとめ：[@antimon2](https://github.com/antimon2)）

---

## どんなもの？

+ SOORL（戦略的オブジェクト指向強化学習）の紹介
    + 自動モデル選択と戦略的探索による効率的な計画
    + 大きな状態空間と疎な報酬のある環境で迅速に探索することを可能にするオブジェクト指向のフレームワーク

---

## 先行研究と比べて何がすごい？

+ DQN: 大量のサンプルが必要
+ OFU?: MDPにうまく適合しない
+ Bayes Adaptive MDP: 大規模なMDPでは手に負えない

---

## 技術や手法の肝は？

+ OOMDP（状態からオブジェクト構造を抽出して有界MDP？）
+ 戦略的探索を用いたオブジェクトレベルの計画アルゴリズム
+ 戦略モデルに基づく強化学習

---

## どうやって有効だと検証した？

+ "Pitfall!" という Atari の（たぶん）一番難しいゲームでテスト・実証
    + https://youtu.be/GvenPZMJiTg (4000 reward) 
    + https://youtu.be/74F-ta5LyuA (2000 reward)

---

## 議論はある？

+ 方向性：不正確なモデルに対して堅牢な計画を立てること
    + 適切なモデルクラスを特定するより重要
+ 改善案：ツリー検索における葉ノードの価値見積を組み込む
    + AlphaGO Zero で実績あり

---

## 次に読むべき論文は？

+ [Mastering the game of Go with deep neural networks and tree search](https://www.nature.com/articles/nature16961) ([PDF](https://deepmind.com/documents/119/agz_unformatted_nature.pdf))
    + AlphaGo Zero の論文
+ [Efficient exploration
through bayesian deep q-networks.](Efficient Exploration through Bayesian Deep Q-Networks)
    + ベイズ線形回帰を介したDQN

