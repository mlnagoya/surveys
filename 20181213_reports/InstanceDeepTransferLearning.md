# A Survey of Deep Transfer Learning
　

### 複数のドメイン間の転移によって新たな価値を見出す→Deep Transfer Learning。（従来の転移学習もその一つ。）
https://arxiv.org/abs/1808.01974

* Instances-based deep transfer learning
 
  ・Targetドメインに転移時、Sourceドメインと類似のデータのみ重み付け   

* Mapping-based deep transfer learning, 

  ・類似の２ドメインのデータを混在させて、別のデータセット

* Network-based（Model-based）deep transfer learning, 

  ・Sourceドメインで大量データにて学習、同じ（または類似の）ネットワークで他ドメインに転移

* Adversarial-based deep transfer learning

  ・敵対する２ドメインのデータから両方に利用できるデータを作る（GANをベースに）

---

# Instance-based Deep Transfer Learning
　
　
https://arxiv.org/abs/1809.02776

### 従来の転移学習（model-based）の精度向上に　instances-based を提案

* 複数ドメイン間のコンビネーションを高め、転移学習の効果をより広く汎用的に

### どんなものか？

* Targetドメインの個々のデータをSourceドメインとのの類似性を確認。
* 精度の低下につながるデータを除去して学習データを最適化するアルゴリズム
* そのうえで従来の転移学習を実施する

#### アルゴリズムについて

* Sourceドメインのモデル（＋重み）に、Targetドメインの訓練データ、検証データを取り込む
* Targetドメインの個々の訓練データを、そのデータがなかった場合と比較してその変化を１つずつチェック
* 損失>0のデータを排除して、訓練データを絞って最適化→Targetドメインの教師データセット　


### 実験１.　Source:拡張MNIST（英文字＋数値）を Target:MNIST(数値)に転移

　手書きの文字と数字では特徴量が類似する

　誤り率による精度比較は以下の通り。

#### 　・　from Scratch 　　1.37
#### 　・　Model-base　　　　　1.09
#### 　・　Instance-base 　　　     0.47

　　※MNISTはすぐに精度が出るのでエポック数=１で実施

### 実験２.　Source:Imagenet　 Target: CIFAR-10 CIFAR-100　　

　　※　学習済みVGG16、ResNet50、DenseNet-121を利用

 
##### 　・                        　　　　　　    (誤り率)  　　　CIFAR-10 　　CIFAR-100 　　　
##### 　・　------------------------------------------------------------- 　 　
##### 　・　from Scratch    　　　　VGG-16    　　  7.81  　　  28.82　　
##### 　・　　　　　　　　　　   　　　ResNet50     　　　6.93    　　27.59
##### 　・　　　　　　　　　　   　　　DenseNet121 　 4.98    　　21.19　　
##### 　・　------------------------------------------------------------- 　
##### 　・　Model-bsd　　  　　　　VGG-16 　　　     7.14   　　 28.01
##### 　・　　　　　　　　　　   　　　ResNet50    　　　 6.20    　　26.90
##### 　・　　　　　　　　　　   　　　DenseNet121  　4.23    　　20.72
##### 　・　------------------------------------------------------------- 
##### 　・　Instance-bsd   　　　　VGG-16      　　　5.01    　　25.29
##### 　・　　　　　　　　　　   　　　ResNet50    　　　 4.11   　　 24.17
##### 　・　　　　　　　　　　   　　　 DenseNet121 　 2.45   　　 18.67

      Figure 1. ResNet23層目。Model-bsdでは誤分類したtest画像が、Instance-bsdで正しく分類しているケースの比較

      Figure 2. VGG-16,ResNet-50,DenseNet-121のCIFAR-10におけるVal-accuracy


### 実験３.　Source:Imagenet　 Target: The Street View House Numbers （SVHN）

　　※　学習済みResNet50、DenseNet-121を利用

　　　　　全く異なるタイプのドメイン間で転移を試した。

##### 　・                        　　　　　　    (誤り率)  SVHN　
##### 　・　------------------------------------------------------------- 　
##### 　・　from Scratch    　　  ResNet-50  　　　 2.12
##### 　・　　　　　　　　　　   　　DenseNet-121  　　　1.83
##### 　・　------------------------------------------------------------- 　
##### 　・　Model-bsd　　  　    ResNet-50    　　　 2.03
##### 　・　　　　　　　　　　   　　DenseNet-121  　　　1.72
##### 　・　------------------------------------------------------------- 　
##### 　・　Instance-based 　　　ResNet-50    　　 1.35
##### 　・　　　　　　　　　　   　　DenseNet-121 　　　 1.12
　＿

### 実験４.　Source:Imagenet　 Target: CIFAR-10 CIFAR-100～不均衡データ　　　



##### 　　CIFAR-10、100の１クラス＝Aを全データの90％、
##### 　　残りのクラス全体を Not Aとして全データの10％の構成。　
　　※　学習済みResNet50、DenseNet-121を利用

##### 　・      　　　　　　　　　   (誤り率)    　　　　　　    CIFAR-10  　CIFAR-100 
##### 　・　------------------------------------------------------------- 　
##### 　・　from Scratch    　　  ResNet-50  　　　　 7.05    　　 28.75
##### 　・　　　　　　　　　　   　　DenseNet-121  　　　5.02     　　21.97
##### 　・　------------------------------------------------------------- 　
##### 　・　Model-bsd　　  　    ResNet-50    　　　　　 6.35     　　28.12
##### 　・　　　　　　　　　　   　　DenseNet-121  　　　5.02     　　21.97
##### 　・　------------------------------------------------------------- 　
##### 　・　Instance-based 　　　ResNet-50    　　 4.18     　　25.87
##### 　・　　　　　　　　　　   　　DenseNet-121 　　　 2.80     　　19.26
　

---

### 議論はある？

転移学習はモデル＋重みを再利用するだけでなく、その応用や精度向上策への研究がさらに広がっている。複数ドメインを掛け合わせて価値を広げる発想は、多品種少量の日本企業向けであることに変わりなく、引き続き見逃せない。
