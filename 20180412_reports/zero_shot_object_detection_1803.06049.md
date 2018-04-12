# タイトル
"Zero-Shot Object Detection: Learning to Simultaneously Recognize and Localize Novel Concepts"[https://arxiv.org/abs/1803.06049](https://arxiv.org/abs/1803.06049)

# どんなもの？
物体検出にzero shot learningの手法を使ったもの


# 先行研究と比べてどこがすごい？
通常の物体検出では、最初から物体のクラスを決めて、そのクラスの物体を検出する。


# 技術や手法の肝はどこ？
## zero shot learning
分類タスクのモデル
inputs → 特徴ベクトル → 既知クラス分類
で、得られる特徴ベクトルで近傍探索する。
ただ、単にこれをすると上手く行かないから、いくらか工夫をする。

## faster-RCNN
画像全体をCNNで一度feature mapにする。
RPN(region proposal network)で物体がありそうな領域を出し、それぞれに対応する特徴ベクトルから分類・回帰を行う

## zero shot object detection
faster-RCNNの物体分類の部分をzero shotなものにする。
特徴ベクトルと既知クラス分類の関係は、word2vecなどのベクトルを使う。

# どうやって有効だと検証した？
ILSVRC-2017のデータセットで検証している。
200クラスからランダムに23クラス選んで既知クラスとして扱って残りのクラスの検出・分類の評価をする
比較したものと比べて良い結果らしい（比較した対象が何かまでは読んでいない）

# 議論はある？
そもそもこの分野は出来立てっぽい。
faster-RCNN以外のYOLOとかSSD系と組み合わせるのもありそう。

# 次に読むべき論文は？
最近のものでZSLで良い物はこれらしい
* L. Zhang, T. Xiang, and S. Gong. Learning a deep embedding model for zero-shot learning.
