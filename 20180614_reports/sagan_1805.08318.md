# タイトル
[Self-Attention Generative Adversarial Networks](https://arxiv.org/abs/1805.08318)

* Han Zhang
* Ian Goodfellow
* Dimitris Metaxas
* Augustus Odena

# どんなもの？
アテンションの機構をGANに使った研究

## 何故読んだ？
1年位前の古いGANの研究では、

* 収束が判断しづらい（そもそも収束するのか）
* 評価が難しい
* パラメータ調整ガチャ
* 訓練し過ぎるとまともな画像を生成しなくなる
* 生成する画像が小さい
で辛い。

使ってみたい方法がいくつかあるので、それ用に最近のGAN研究の状況の把握したい。

# 先行研究と比べてどこがすごい？
GANの文脈でアテンションの技術が試されていなかった。
FIDやISの指標でSOTA。

# 技術や手法の肝は？
## アテンション
ある層のそれぞれの点に対してその層全体のどこを注目するかを意味するattention mapを作り、その重みを使って全体から特徴を取り出す。得られるfeature mapをres blockの残差の部分として使う。これをgenerator,discriminatorの両方で利用。

c.f. [Non-local Neural Networks https://arxiv.org/abs/1711.07971](https://arxiv.org/abs/1711.07971)

アテンション無し、有り、res-blockの3ケースをアテンション等を入れる層を変えながら効果を見ると、ある程度深い層で入れると効果があることが分かった。

似たように見える手法でAttnGANがある。AttnGANは、テキスト入力として画像を生成するもので、単語に対してどこを注目するかという構造になっている。SAGANは自身の層の点から点への注目をするという点で異なり、selfという単語が使われているっぽい。

## 訓練の安定化
### SNGAN
[Spectral Normalization for Generative Adversarial Networks https://arxiv.org/abs/1802.05957](https://arxiv.org/abs/1802.05957)

spectral normに制限を与えてLipschitz constantを制御する手法spectral normalizationを利用。
* ハイパーパラメータ探索が実質不要
* 計算コスト低

### TTUR
[GANs Trained by a Two Time-Scale Update Rule Converge to a Local Nash Equilibrium https://arxiv.org/abs/1706.08500](https://arxiv.org/abs/1706.08500)

generatorとdiscriminatorの学習率を揃えずに訓練する方法。discriminatorに正則化をすると訓練が遅くなる傾向があったのを改善した。

## 評価指標
次の指標をランダム生成した画像5万枚に対して算出。
ImageNetの画像で画像サイズを128x128にして訓練。(conditionalな画像生成タスクとして)

### Inception score(IS)
訓練済みモデルではっきりと分類できるかどうかで評価する。
高い方が良い。

### Fréchet Inception distance(FID)
訓練済みモデルの途中の層を特徴ベクトルの分布を生成したものと訓練データとで比較した値。
Inception-v3の最後のpooling層を利用。
低い方が良い。

## 可視化
generatorのアテンションが使われている最も後の層を可視化。対象のピクセル毎に、注目領域をヒートマップとして生成した画像と共に表示。

# どうやって有効だと検証した？
## 指標
ISとFIDがかなり改善
|      |  IS  |  FID  |
| SNGAN-projection  |  36.8  |  27.62  |
| SAGAN |  52.52  |  18.65  |

## 訓練
訓練時の損失関数の値が理想的に下がる。（訓練し過ぎると損失の値が急に上がる現象がないようなグラフ）

ISも訓練時に算出して、これも理想的に増えていく。

# 議論はある？
## 私見
GANは分類モデルなどがあれば評価可能な状態。

GANに限らず、他でも使えそうな技術がある。

# 次に読むべき論文は？
* [SNGAN](https://arxiv.org/abs/1802.05957)
* [Non-local Neural Networks](https://arxiv.org/abs/1711.07971)
