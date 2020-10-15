# Mesh Guided One-shot Face Reenactment Using Graph Convolutional Networks
[https://arxiv.org/pdf/2008.07783.pdf](https://arxiv.org/pdf/2008.07783.pdf)
(まとめ @strshp)

著者
- Guangming Yao
- Yi Yuan
- Tianjia Shao
- Kun Zhou
(NetEase Fuxi AI Lab, State Kye Lab of CAD&CG, Zhejiang University)

## どんなもの？
![](meshguided_oneshot_face_reenactment/figure1.png)
- ターゲット画像の表情をソース画像に適用するモデル
- [同じタスクを解く別手法(MarioNETte)のデモ](https://www.youtube.com/watch?v=Y6HE1DtdJHg)

## 先行研究の弱点
- GANベースの手法では、生成される画像のクオリティは高いものの、学習には同一人物の画像が大量に必要だった。別の人物に適用する場合には、再学習が必要だった
- 顔のキーポイントを利用してソース画像からターゲット画像へのOpticalFlowを求め、それを元にソース画像を変形する方法も提案されていたが、
ソース画像とターゲット画像で顔の形が違うため、ソース画像の顔が上手く保持されないという難点があった
- 顔のキーポイントは疎であるため、表情の細かい部分の情報が抜け落ちてしまっている。そのため、生成された画像はターゲット画像の表情を完全には再現できない
- 最新の研究では、LandmarkTransformer(?)を使ったFew-shotの手法が提案され、上記の手法の問題点に対処したが、まだ品質が完全とは言えなかった

## 先行研究と比べて何がすごい？
- 学習に使っていない画像に対しても適用可能
- 先行研究で提案された手法よりも、定量的にも定性的にも高品質な結果が得られる

## 技術や手法の肝は？
### 概要
- 処理の途中で扱う顔の表情や頭部の姿勢情報を「キーポイント」ではなく「メッシュ」として保持することで、生成画像のクオリティを高めた
- ソース画像の変形に用いるOpticalFlowをメッシュを使って生成したり、オクルージョンを意識してめちゃくちゃ丁寧に生成

![](meshguided_oneshot_face_reenactment/figure2.png)

### MeshRegressionModule
- ソース画像とターゲット画像に対するメッシュを生成するモジュール
  - 既存モデル(3DMM regressor)を使って、画像から表情(exp)、見た目(id)、頭部姿勢(pose)をエンコードしたベクトルを抽出
  - 抽出したベクトルから、既存モデル(?)を使ってメッシュ(頂点ベクトルと隣接行列)を生成
  - ソース画像とターゲット画像それぞれに対して上記の処理を行うことで各画像に対してメッシュ(M_s, M_t)を生成
    - このとき、ターゲット画像のIDをソース画像のIDに置き換えることで、ターゲット画像の顔の形状を無視できると主張
  
### MotionNet
- 2つのメッシュ間から、2画像間のピクセルの移動を表すOpticalFlowを生成するモジュール
  - GCNを使って(M_s, M_t)から2画像間の動きをエンコードしたベクトル(F_m: Motion Feature)を生成
  - 残差構造を利用したデコーダーネットワークで、F_mからOpticalFlow(Γ*)を生成

### Reenacting Module
- OpticalFlowとソース画像を元に、ソース画像にターゲット画像の表情と頭部姿勢を適用した画像を生成するモジュール
![](meshguided_oneshot_face_reenactment/figure3.png)
  - aa


## どうやって有効だと検証した？
### 定性評価
![](meshguided_oneshot_face_reenactment/figure4.png)

### 定量評価
![](meshguided_oneshot_face_reenactment/table1.png)
---



## 議論はある？
- 特になし

## 次に読むべき論文は？
[Graph Neural Networks](https://arxiv.org/pdf/1812.08434.pdf)
[Regressing Robust and Discriminative 3D Morphable Models](https://openaccess.thecvf.com/content_cvpr_2017/papers/Tran_Regressing_Robust_and_CVPR_2017_paper.pdf)


+ Reference の他の論文で読んだ方が良さげなものをピックアップ
+ [Web で公開されている論文ならリンクにする](https://arxiv.org/pdf/1710.05941.pdf)
    + サブリストでそれがどんな論文か一言あるとBetter