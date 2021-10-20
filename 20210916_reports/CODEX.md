# TransReID: Evaluating Large Language Models Trained on Code

https://arxiv.org/abs/2107.03374

(まとめ Saito)

すいません、ところどころ理解できてない（間違い書いてるかも）

著者

- Mark Chen, 他たくさん　 OPEN AI
  github と Azure のサポート有

# どんなもの？

GPT ３元に、docstrings から python code を生成（成果率アップ）<br>
https://openai.com/blog/openai-codex/　ここで、API を試せる<br>
プログラム作れる＝ AI 作れるのも時間の問題？<br>
OPENAI は総合的にそこ目指している気がする。<br>

以下のような点について記載<br>

評価方法も提案（BLUE ではだめ）、データセットも作成、問題(prompt)結構難しく見えるの解いてる<br><br>
繰り返しサンプリングで unit test 正解率高い(70.2%)<br>
デモで、アニメや PON みたいなゲームも作成していたよう<br>
sandbox で安全確保<br>
code fine turning<br>
supervised fine turning<br>
docstings generation<br>
limitation<br>
この技術のインパクトについて<br>
関連 work<br>
<br>

# 以下気になった図表について <br>

![1](codex/F1.png)

# モデルが大きいほうが Unit test 正解率高い x

codex-S（oracle としていいの選ぶと）８０％近い正解<br>
GPT のころからモデル大きければよくなるとの予測が今も続いている<br>
（ムーアの法則レベルか）<br>

#

![2](codex/F2.png)

# docstring から python 作っている例（結構難しいのもできてる）<br>

![3](codex/F3.png)

# 測定基準　 pass@k の式と def <br>

![4](codex/F4.png)

# 上から <br>

抜き出すサンプル数増やすと Pass@K よくなる + Temperature との兼ね合い示す<br>
抜き出すサンプル数増やすと Temperature 大きいほうがいい <br>
model 大きいほうが pass@k 良くなる <br>

![5](codex/F5.png)

# 左　サンプル数と Pass rate 関係（サンプル方法で系列別） <br>

# 右　 BLEU スコアは機能成否を表していない <br>

BLEU は、正解がいくつか用意されているなかで、modified precision と recall で評価しているが、recall とかは文字列長が短いとペナルティで、コードを簡潔にかくとペナルティに
なると思われる。<br>
precision の方でも、天才的に実装すると低くなる可能性があると思える。

![6](codex/F6.png)

# モデル、サンプル数、サイズ別　 pass@k <br>

![7](codex/F7.png)

# 関数の呼び出し階層が深いと難しい <br>

![8](codex/F8.png)

# 学習の？docstring にバグがあると pass@1 は悪くなる <br>

#

# 先行研究と比べてどこがすごい？

正解率高い（GPT ３はほぼ 0%)<br>
結構難しいのも作っている<br>

# 技術や手法の肝は？

1 GPT で、一つのモデル、事前学習＋少しの調整（もしくは調整なし）でもいろんなタスクで SoTa だした流れ<br>
GPT2 で、なんでもできるの作ろうの流れで、されにモデルを大きくした GPT3 がでてきた<br>
GPT3 でもコードは作れたみたいだが、やはりまだ精度が低い<br>
そこで、データ（コンペサイト、CI）を用意し、unit test 方式や細かい調整して劇的に精度上げた。<br>
文章理解、生成とコードの生成では、要求される創造性のレベルが違うのかなと思った。<br>

2 　 BLEU では機能評価低いので、新たな指標（unit test pass)作成<br>

3 モデルは大きいほうがいい（GPT からの歴史が継続中）RNN とかはそうとは言いきれないらしい<br>

4 AI が作成した不確かなコードを安全に動かす環境作成<br>

# 議論はある？<br>

unit test でパフォーマンスやセキュリティ担保とか、ＡＩが作ったコードを安全に動かす<br>
環境が作れるか？でしょうか？<br>

# 私見<br>

AI がプログラム作れる　＝　 AI 作れる　＝　進化止まらない　シンギュラリティ！！　ってことでわくわくする。怖がったほうがいいかもですが。

OpenAI が提供する GPT 調整済みモデルをいくつか見た。Instruct series が今のところ<br>
面白い、指示を細かく付け加えていくとそれに応じて、出力変えてくる。<br>

改めて transformer からの系譜の有名なところ確認したい<br>

GAFA などがなどが学習済みの小さななんでも強いモデルを提供してくれたらうれしい<br>

# 次に読むべき論文は？

Transformer<br>
BERT,XLNet,RoBERT,Distributed BERT<br>
GPT,GPT2,GPT3<br>
Vit,DETR<br>
