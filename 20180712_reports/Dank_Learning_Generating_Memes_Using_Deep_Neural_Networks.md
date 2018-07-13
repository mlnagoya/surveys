# Dank Learning: Generating Memes Using Deep Neural Networks

2018/06/07 Abel L Peirson V, E Meltem Tolunay

https://arxiv.org/abs/1806.04510

（まとめ：@Denpa92）
***************************************************

### どんなもの？

- ネタ画像から面白いCaptionを生成する手法の紹介。

- 中身がGoogleのShow and Tellモデルの改良版。

-  画像に説明タグを付与することで、生成したCaptionの多様性が向上した。
***************************************************

### どうやって有効だと検証した？

- Perplexity（正解候補数）

- 人間による採点
  - 既存のCaptionと生成したCaptionとの識別度
  - Caption自体の面白さ
***************************************************

### 技術や手法の肝は？

- 3種エンコーダモデルのパフォーマンス比較：
   1. 画像のみ ([Inception-v3](https://i.kym-cdn.com/photos/images/original/000/384/176/d2f.jpg))
   2. 画像+説明タグ（Glove-Average）
   3. 画像+説明タグ（Attention）
***************************************************

### 議論はある？

- Captionのバリエーションが説明タグのセンスに依存。

- 人種差別、性的差別発言問題。

***************************************************
### 先行研究と比べて何がすごい？

- 説明タグの追加することでより正確にユーモアの特徴を抽出できる。

- 本物のものと差別化できないネタ画像の作成を自動化できる。
***************************************************
### 次に読むべき論文は？

- [Humor recognition and humor anchor extraction.](https://aclanthology.info/pdf/D/D15/D15-1284.pdf)
  - 文章を面白くする要素の認識&抽出

- [Are Word Embedding-based Features Useful for Sarcasm Detection?](https://arxiv.org/abs/1610.00883)
  - 単語埋め込みに基づく特徴は皮肉検出
***************************************************




