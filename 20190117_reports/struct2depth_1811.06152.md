# Depth Prediction Without the Sensors: Leveraging Structure for Unsupervised Learning from Monocular Videos,
[https://arxiv.org/abs/1811.06152](https://arxiv.org/abs/1811.06152)
(まとめ @n-kats)

著者
* Vincent Casser
* Soeren Pirk
* Reza Mahjourian
* Anelia Angelova

# どんなもの？
動画を入力して訓練させると depth 推定をしてくれるモデル。

とりあえずありものの手法を組み合わせてベースラインのモデルを作成。
さらに"Motion Model"と"Refinement Model"を追加し、性能改善。

1080tiで数十FPS

# 先行研究と比べてどこがすごい？
depthを認識するためにego-motion（カメラの動き）も認識する手法を、
* 動体の認識
* テスト時の訓練
で改善。動体や前方にある車のdepth推定が特に改善

（訓練の詳細は[先行研究参照](https://people.eecs.berkeley.edu/~tinghuiz/projects/SfMLearner/)）

# 技術や手法の肝は？
## Baseline
複数の画像とその内部パラメータから、ego-motionのパラメータを認識する。
* 画像からdepthを認識
* depthと予想されるego-motionから画像を移動前の位置からのものに変換
* 目的の画像が生成できるように訓練
* 推論の滑らかさを表す損失も追加
  * SSIM
  * SM

## Motion Model
背景（移動しないもの）と車などの移動体を分離し、背景及びそれぞれの移動体毎に移動方向を割り出す。
![](./struct2depth_1811.06152/compare.png)

動体の認識に Mask RCNN を利用しているように書いてあるように思うが、公開されているコードがそうなっていないように見える（要確認）

## Object Size Constraints
サイズ制約

クラス毎に動体の大きさを決め打ちする。depthがそれとできるだけ矛盾しないように訓練。

## Refinement Model
教師なしだから、評価実行時にも訓練ができる。別データセットで訓練後、評価用データでそれをやると良くなる。

![](./struct2depth_1811.06152/refine.png)
（左はKITTI, 右はcityscape, これらはKITTIで訓練）小さいものが取れているように見える

# どうやって有効だと検証した？
![](./struct2depth_1811.06152/table.png)

KITTI, Cityscapes, Fetch Indoor Navigation (最後は屋内)のデータセットで分析。

コードが[https://github.com/tensorflow/models/tree/master/research/struct2depth](https://github.com/tensorflow/models/tree/master/research/struct2depth)に公開されている。
ただし、色々修正しないと動かないかも. 

# 議論はある？
* 多数のフレームを利用
* 今回のモデルを使って3D再構成
とかをしてみたいらしい

## 私見
KITTIみたいな前方カメラならともかく、変な角度の映像で上手く行くのか心配
# 次に読むべき論文は？
* [https://people.eecs.berkeley.edu/~tinghuiz/projects/SfMLearner/cvpr17_sfm_final.pdf](https://people.eecs.berkeley.edu/~tinghuiz/projects/SfMLearner/cvpr17_sfm_final.pdf)  
  先行研究。訓練の詳細が分かるかも
