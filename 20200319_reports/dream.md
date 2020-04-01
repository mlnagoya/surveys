Introducing Dreamer: Scalable Reinforcement Learning Using World Models  
===

Posted by Danijar Hafner, Student Researcher, Google Research 


[Google AI Blog Wednesday, March 18, 2020](https://ai.googleblog.com/2020/03/introducing-dreamer-scalable.html?m=1)  
[Paper](https://arxiv.org/pdf/1912.01603.pdf)  

---

## どんなもの？

* モデルベースの強化学習アルゴリズム  
* VAEを時系列に連結した構成  
  1) World Modelの学習入力イメージからエンコーダを学習)。  
  2) 価値関数とActorネットワークの学習  
  3) 行動  
  の流れで学習を進める。

  
[イメージ図 (ブログ参照)](https://1.bp.blogspot.com/-4J0POdpDz8U/XnFFZ_POSXI/AAAAAAAAFfg/3Dzzf-nbPUQuYWiJuzbZK__vfjHTjYtrQCLcBGAsYHQ/s1600/image2.png)



---

## 先行研究と比べて何がすごい？  

* モデルベースの手法で、3Dコントロールタスクのような連続な探索空間を対象とする課題で良い結果が得られた。  
  モデルフリーで方策ベースの手法で検討されることが多いタスク。
  比較対象としてもD4PG、A3Cなどの方策ベースの手法と比較。 

* 類似の手法としてWorld Models(2018) → Deep Planning Network(PlaNet) (2019) → Dreamer の流れで発展している。  


---

## どうやって有効だと検証した？  

* DeepMaind Control Suiteによる、3Dコントロールタスクによる評価。  
  
類似のモデルベース手法としてDreamerとPlaNet、モデルフリー手法としてD4PGとA3Cの間で比較を行った。

[結果グラフ (ブログ参照)](https://1.bp.blogspot.com/-7CZawd00x4M/XnFFZzSu9jI/AAAAAAAAFf4/EvlvcxNhcr8dv4lq2ZJP6Gc9HRtcFVvEgCEwYBhgL/s1600/image1.png)


---

## 技術や手法の肝は？

* 環境からイメージを入力して、特徴量を抽出。 → 特徴量からの予測で行動価値関数・状態価値関数の学習を進める。
* VAEの隠れ層を、時系列に連結して「予測」と「行動」列を生成する。    

---

## 議論はある？

* 連続制御タスクで、モデルフリーの手法と比較して良い結果を出した。  
* ゲーム等の単純なイメージ入力では無く、複雑なイメージが入力された場合へ応用できるか？  

---

## 次に読むべき論文は？

* [Planet](https://ai.googleblog.com/2019/02/introducing-planet-deep-planning.html)  
* [World Models](https://arxiv.org/abs/1803.10122)  


