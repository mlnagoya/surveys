Learning and Querying Fast Generative Models for Reinforcement Learnin
===

2018/02/08  Lars Buesing, Th'eophane Weber, S'ebastien Racani'ere, S. M. Ali Eslami, Danilo Rezende, David P. Reichert, Fabio Viola, Fr'ed'eric Besse, Karol Gregor, Demis Hassabis, Daan Wierstra

[https://arxiv.org/pdf/1802.03006.pdf](https://arxiv.org/pdf/1802.03006.pdf)

（まとめ：@kmiwa）

---
## どんなもの？・手法
- 状態空間モデルを使って強化学習の手法。パフォーマンスを向上させる

---
## 貢献
- 決定論的状態空間モデル（dSSM）と確率論的状態空間モデル（sSSM）の比較を行った
- 対数尤度を使ってモデルの精度を計算した
- パックマンでの効果的なパフォーマンスの向上を示した

---
## どうやって有効だと検証した？
- Arcade Learning Environmentの４つのゲームにて検証
![](https://i.imgur.com/VkHGZLq.png)


---

## 技術や手法の肝は？
- 状態空間モデル
-- 状態を表すモデルで２本のモデルより成り立つ
![](https://i.imgur.com/zHoJNSa.png)
- 決定論的状態空間モデル
-- 何回やったところで同じ結果が得られる
- 確率論的空間状態モデル
-- シミュレーションごとに結果が異なる 
- 決定論的状態空間モデルで、さらにdSSM-DET（e deterministic decoder）とdSSM-VAE（ stochastic decoder）を定義する
- 各構造は以下のようになる
![](https://i.imgur.com/EEtcUCF.png)
*□はdeterministic nodes。◯は乱数。●は訓練中に計測された変数
*RARは、recurrent auto reguression model


---

## 議論はある？
- I2A(Imagination-Augmented Agents)を採用して、環境モデルの推定を行った。I2Aは、不正確なプランニングから使える情報をニューラルネットを利用して抽出する。

---

## 先行研究と比べて何がすごい？
- データに欠損値があっても使えるという特徴を持つ状態空間モデルを採用することで、パフォーマンスの向上を示した

---

## 次に読むべき論文は？
- [Imagination-Augmented Agents for Deep Reinforcement Learning](https://arxiv.org/pdf/1802.03006.pdf)


