Universal Spike Classifier
===

2018/11/7 Muhammad Saif-ur-Rehman, Robin Lienkämper, Yaroslav Parpaley, Jörg Wellmer, Charles Liu, Brian Lee, Spencer Kellis, Richard Andersen, Ioannis Iossifidis, Tobias Glasmachers, Christian Klaes

[https://arxiv.org/abs/1811.02923](https://arxiv.org/abs/1811.02923)

（まとめ：@nharu1san）

---

## どんなもの？
+ CNNを用いて脳電位の分類(Spike or Artifacts)を行った

### Artifacts, Spike
![表1](https://i.imgur.com/Uni665J.png)

---

## 先行研究と比べて何がすごい？
+ これまで手動もしくは半自動で行なっていた作業の自動化

---

## 技術や手法の肝は？
+ CNN
![構成図](https://i.imgur.com/KKPy2zC.png)

---

## どうやって有効だと検証した？
![比較結果図](https://i.imgur.com/oDOmXnT.png)
+ Utah電極やマイクロワイヤーで計測した電位データを使用
+ 主成分分析をしてラベル付けした物を教師データとする


---

## 議論はある？
+ ノイズ分別のみ
+ Multi Unitへの適用

---

## 次に読むべき論文は？
+ [A fully automated spike sorting algorithm using t-distributed neighbor embedding and density based clustering](https://www.biorxiv.org/content/early/2018/09/26/418913)
  - spikeの分類アルゴリズムについて
