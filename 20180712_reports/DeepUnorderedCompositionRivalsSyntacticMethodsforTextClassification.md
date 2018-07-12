Deep Unordered Composition Rivals Syntactic Methods for Text Classification
===

2015 Mohit Iyyer(University of Maryland, Department of Computer Science and UMIACS), Varun Manjunatha(University of Maryland, Department of Computer Science and UMIACS), Jordan Boyd-Graber(University of Colorado, Department of Computer Science), Hal Daume ́ III(University of Maryland, Department of Computer Science and UMIACS)

[http://www.aclweb.org/anthology/P15-1162](http://www.aclweb.org/anthology/P15-1162)

（まとめ：@nharu1san）

---

## どんなもの？
+ テキストの順番を考慮しない構文処理モデル

---

## 先行研究と比べて何がすごい？
+ 他のモデル(RecNN)と比べても結果に遜色がなく、実行時間が短い

---

## 技術や手法の肝は？
![図1](https://i.imgur.com/pKylMKE.png)
+ 各入力を平均し、フィードフォワードネットワークへ入力する
+ ワードドロップアウト
  + 通常のドロップアウトの代わりにベクトル平均からランダムに入力単語を削除する
  + RecNNには効果なし

---

## どうやって有効だと検証した？
![表1](https://i.imgur.com/FZYUs8R.png)
+ 感情分析
  + SST
  + RT
  + IMDB
+ QAタスク
  + Iyyerらの行った歴史に関するQAタスクを実施
  + QANTAと呼ばれるRecNNと比較し、Wikipediaのデータを加えた学習時に上回った

---

## 議論はある？
![図2](https://i.imgur.com/cyrbUHS.png)
+ 二重否定などに弱い
  + DRecNNの方がわずかに良い

---

## 次に読むべき論文は？

