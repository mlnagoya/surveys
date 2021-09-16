# TransReID: Evaluating Large Language Models Trained on Code
https://arxiv.org/abs/2107.03374

(まとめ @ma)

すいません、おもしろそうと思い選んだのですが、理解きちんとできていない。間違って解釈もありそう。

著者
* Mark Chen, 他たくさん　OPEN AI
githubとAzureのサポート有

# どんなもの？
GPT３元に、docstringsからpython codeを生成（成果率アップ）
https://openai.com/blog/openai-codex/　ここで、APIを試せる

以下のような点について記載

評価方法も提案（BLUEではだめ）、データセットも作成、問題(prompt)結構難しく見えるの解いてる
繰り返しサンプリングでunit test正解率高い(70.2%)
デモで、アニメやPONみたいなゲームも作成していたよう
sandbox(gVisitor?)で安全確保
code fine turning
supervised fine turning
docstings generation
limitation
この技術のインパクトについて
関連work

# 先行研究と比べてどこがすごい？
正解率高い（GPT３はほぼ0%)
結構難しいのも作っている

# 技術や手法の肝は？

1 BLUEでは、マッチング見ているが、機能的正解、不正解とマッチしていない
  unit test,人間が判断がいい
2 何回もサンプリングかつ高いtemperatureで、unit testを通すものが（一つでも）できる
  確率が高くなる Page5 figure5
3 モデルは大きいほうがいい Page5 figure4
4 たくさん作るが一つだけ評価する場合　Page6　figure7 (以下の順で良い成果）
   1)oracle with prior knowledge of the unit tests
　 2）highest mean log-probability (red) 
　 3) highest back-translationscore (orange) < randomと同じくらい
５ Page6 figure8 Note that the distributions are not cleanly separable
   BLEUは評価に適さない
６ Pass@k nunbiased estima を定義（式とpython function) Page3
7  evaluation framework at https://www.github.com/openai/human-eval. Page2
    164 original programming problems
8 教師あり学習
　コンペサイト使用、CI使用
　Page9 Figure9 でよくなっているのわかる
9 Docstring Generationは難しい？
10 トークナイザー　空白を長さ別に別tokenにした
11 労働市場、環境、法、等々も言っている

# 議論はある？
  unit testでパフォーマンスやセキュリティ担保とか、ＡＩが作ったコードを安全に動かす
  環境が作れるか？でしょうか？

## 私見

OpenAIが提供するGPT調整済みモデルをいくつか見た。Instruct seriesが今のところ
面白い、指示を細かく付け加えていくとそれに応じて、出力変えてくる。

# 次に読むべき論文は？
  transformer
  BERT
  GPT
