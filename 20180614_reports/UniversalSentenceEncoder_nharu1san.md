Universal Sentence Encoder
===

2018/03/29 Daniel Cer(Google Research), Yinfei Yang(Google Research), Sheng-yi Kong(Google Research), Nan Hua(Google Research), Nicole Limtiaco(Google Research), Rhomni St. John(Google Research), Noah Constant(Google Research), Mario Guajardo-Cespedes(Google Research), Steve Yuan(Google), Chris Tar(Google Research), Yun-Hsuan Sung(Google Research), Brian Strope(Google Research), Ray Kurzweil(Google Research)

[https://arxiv.org/abs/1803.11175](https://arxiv.org/abs/1803.11175)

（まとめ：@nharu1san）

---

## どんなもの？
![図1](https://i.imgur.com/mRkO7OU.png)
+ 文情報のエンコードモデル
+ 精度とコストのトレードオフによりTransformer, DANの二種類のバリエーションが存在
  + Transformer: VaswaniらのTransformerモデルを利用. (精度高-コスト重)
  + DAN: IyyerらのDeep Averaging Networks(DAN) というモデルを利用. (精度低-コスト軽)

---

## 先行研究と比べて何がすごい？
+ 文章レベルの埋め込みであること

---

## どうやって有効だと検証した？
![図2](https://i.imgur.com/UhrX1o0.png)
+ 映画レビューやカスタマーレビューの分類タスク用のDNNに対して入力したスコアの比較
  + USEを使わないword embeddingのみの場合, USEのみ, USE+word embeddingの比較
  + 学習データ数による結果の比較
  + 文長とUSEが使用するCPU, GPU, Memoryの比較
+ Word Embedding Association TaskのGloVeとの比較

---

## 技術や手法の肝は？
+ Transformer
![図3](https://i.imgur.com/a7mmUAz.png)
畳み込みや再帰のない注意モデル

+ DAN
![図4](https://i.imgur.com/ODvHSMa.png)
単語ベクトル入力を平均化しDNNへ入力するモデル

---

## 議論はある？
![図5](https://i.imgur.com/I8jHt5z.png)
+ 計算時間はTransformerモデルがnの二乗, DANはnのオーダー
  + リソースに応じて選択を
+ WEATタスクの一部でGloVeよりも低い値
  + 訓練データと訓練タスクの違いに起因？

---

## 次に読むべき論文は？
+ [Attention Is All You Need](https://papers.nips.cc/paper/7181-attention-is-all-you-need.pdf)
  + Transformerについて
+ [Deep Unordered Composition Rivals Syntactic Methods for Text Classification](http://www.aclweb.org/anthology/P15-1162)
  + DANについて


