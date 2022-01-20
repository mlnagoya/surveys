# Projected GANs Converge Faster

Axel Sauer<sup>1,2</sup>&emsp;Kashyap Chitta<sup>1,2</sup>&ensp;  Jens Müller<sup>3</sup>&ensp;  Andreas Geiger<sup>1,2</sup> 

<sup>1</sup>University of Tübingen&ensp;<sup>2</sup>Max Planck Institute for Intelligent Systems, Tübingen  

<sup>3</sup>Computer Vision and Learning Lab, University Heidelberg

https://arxiv.org/pdf/2111.01007.pdf

## どんなもの？

- 事前学習した特徴抽出器を GAN での画像生成にも有効活用したもの

- 事前学習モデルが出力する特徴量を最大限に活用するため、Discriminator の入力に feature pyramid と、入力空間へのランダムな射影を用いた

## 先行研究と比べて何がすごい？

- ランダムなノイズから画像を生成する GAN の枠組みの中では、初めて事前学習モデルの有効活用に成功した

- 縦横1024ピクセルの解像度に対応し、21のデータセットにおいてSOTAを更新するか、従来のSOTAに匹敵する

- 従来のSOTAに比べて40倍高速で、5日訓練して到達できるFIDに3時間以下で到達できる

<img src="converge_faster.png" title="" alt="converge_faster" data-align="center">

## おさらい

- GAN は Generator と Discriminator の2つのネットワークを訓練する

- Generator は低次元のノイズ（正規分布から生成）を入力として受けとり、画像を生成する

- Discriminator は画像を入力として受けとり、その画像が実在する画像か、Generator によって生成された偽の画像かを予測する

- Generator と Discriminator を交互に学習させて、両方賢くなれば、いずれ Generator は実在する画像と見分けがつかない画像を生成するようになるはず

- 以下の目的関数を最小化する

<img src="gan-objective.png" title="" alt="gan_objective_" data-align="center">

## 技術や手法の肝は？

- 事前学習モデルの特徴量を最大限活用するために：
  
  - 事前学習モデルの各レイヤーの特徴量を、それぞれ異なる独立した Discriminator に入力した

- Discriminator が特徴空間の部分集合にのみ注目しないように:
  
  - Discriminator に上記の特徴量を入力するのではなく、特徴量をミックスしたり、ランダムに射影した特徴量を入力とした

### Multi-Scale Discriminators

- Discriminator の入力に画像を与えるのではなく、学習済みの特徴抽出器が出力した特徴量を与える

- 特徴抽出器の各レイヤーが出力する特徴量のうち、64<sup>2</sup>、32<sup>2</sup>、16<sup>2</sup>、8<sup>2</sup>の解像度のものを、それぞれ D<sub>1</sub>、D<sub>2</sub>、D<sub>3</sub>、D<sub>4</sub>の入力とする

- 損失計算時はすべてのD<sub>l</sub>に関して加算したものを求める

### Random Projections

- Discriminator はより意味的な特徴を捉えておらず、分かりやすい特徴のみに注目することが実験で観察された

- 分かりやすい特徴を弱めるために、微分可能なランダム射影を用いて特徴量をミックスするモジュールを導入した

- 「微分可能なランダム射影」の関数には畳み込みを用いるが、ランダム性を保持するために重みは更新されない

#### Cross-Channel Mixing (CCM)

<img title="" src="ccm.png" alt="ccm.png" data-align="center" width="226">

- ランダムな射影によって、特徴の情報が射影前から失われることなく、かつ自明な変換でない一番簡単な方法は 1x1 Conv である

- 畳み込みの重みは He の手法で初期化し、訓練中にこの重みは一切更新されない

- 活性化関数も用いない

#### Cross-Scale Mixing (CSM)

<img title="" src="csm.png" alt="csm.png" data-align="center" width="252">

- 空間方向の特徴をミックスするモジュールとして、U-Net と同様のアーキテクチャを用いた

- これも重みは He の初期化を用いる

#### Pretrained Feature Network

- 特徴抽出器はいろいろなサイズを試した
  
  - EfficientNet、ResNet の様々なサイズのモデルと、ViT

- 実験の結果、より小さいモデルの方がより低いFIDを得ることができた
  
  - このことから、よりコンパクトな表現のほうが良いことがわかる

- コンパクトなモデルで済むので、計算速度もその分向上した

- また、事前学習の有効性を示すため、ランダムな重みで初期化して実験してみたら、FIDの値は高くなった
  
  - やっぱり事前学習が有効



上述の施策によって、従来の GAN とは異なり、複数の Discriminator やランダム射影などのコンポーネントが追加されたため、目的関数も下記のように変更する

<img src="pgan_objective.png" title="" alt="pgan_objective.png_" data-align="center">

## 結局どの施策が有効だったの？ (Ablation Study)

<img src="fid_table.png" title="" alt="fid_table.png_" data-align="center">

### どの特徴抽出器のレイヤーが有用な特徴量を出力するのか？

- （表の一番上、'No Projection' のところ）有用な特徴量を知るために、L<sub>1</sub>からL<sub>4</sub>までの特徴をいろんな組み合わせで用いた

- 表の値は RGB 画像を Discriminator の入力として学習させたときに得られた FID で、特徴抽出器の特徴量を Discriminator の入力として学習させたときに得られたFIDを割ったもの

- 特徴抽出器を用いた場合、値が大体1を下回っており、画像を入力するよりも良いことがわかる

- 興味深い点は、Discriminator を追加していくにつれて性能が悪くなっていくところ
  
  - より意味的な特徴は直接ロスに関わらない



### どうしたら最も有効に特徴量を利用できるか？

- CCMを導入すると、FIDを大幅に向上させることができたが、深い層の特徴は未だに有効に扱えていないことがわかる

- CSMを導入すると、4つの Discriminator を組み合わせたときに最もよいFIDを得られることがわかった。
  
  - CSMによって深い層の特徴をよく使えるようになったと著者は主張
  
  - ちなみに、CCM + CSM に画像を突っ込むと性能が低下するらしい



## どうやって有効性を示した？

- 実験で従来のSOTAと実行速度、FIDの値で比較した



### 実行速度

<img src="train_prop.png" title="" alt="train_property.png_" data-align="center">

### FID

![fid_res.png_](fid_res.png)