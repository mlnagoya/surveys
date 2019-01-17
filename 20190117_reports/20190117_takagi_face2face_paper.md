A face to face neural conversation model
===

Hang Chu, Daiqing Li, Sanja Fidler

http://www.cs.toronto.edu/face2face  
http://www.cs.toronto.edu/face2face/media/face2face_paper.pdf  
（まとめ：HisashiTakagi）

---

## どんなもの？

+ テキストもしくは動画による会話文の入力に対して、自然言語による返答
+ 同時にそれに合う適切な顔のジェスチャを生成するニューラルネットワークモデルを提案
+ テキスト情報と顔情報の両方を用いた適切な応答の生成を可能にした

---

## どうやって有効だと検証した？

+ Mind-Reading test
    + モデルがうまくテキストと表情を生成できるか？
    + ５種類の比較
+ TheNeuralHank Chatbotの実装
    + 3つのモデルで比較

---

## 技術や手法の肝は？

+ NNでデコードとエンコード
+ 2レイヤーでデコード　６モジュール
+ 訓練は教師データに映画。
+ より自然な対話ができるアバターを実装

---

## 議論はある？

+ 仮想アバターを使ったが将来はパーソナリティをもち全身があるようなものが目標 。
+ デモを見ると会話が成立しているかもしれない感あり

---

## 先行研究と比べて何がすごい？

+ テキストだけ従来ー顔の表情も同時に生成

---

## 次に読むべき論文は？

+ T. Baltrusaitis, P. Robinson, and L.-P. Morency. Openface:
an open source facial behavior analysis toolkit. In WACV,
pages 1?10, 2016. 2, 3, 4
