# YOLOX: Exceeding YOLO Series in 2021
https://arxiv.org/abs/2107.08430

(https://zenn.dev/takoroy/articles/e1e401b865f6c1も参考にしました)

(まとめ @masahiro6510)

### 出版年月
2021年8月

### 著者
Zheng Ge∗ Songtao Liu∗† Feng Wang Zeming Li Jian Sun
Megvii Technology

## どんなもの？
![Alt text](yolox_fig/image.png)
- YOLOシリーズの改良版としてYOLOXを提案
    - YOLO検出器をアンカーフリーにした
- 開発者や研究者が使いやすくするために公式リポジトリで、ONNX、TensorRT、NCNN、Openvinoに対応したデプロイ版も提供されている。(htt
ps://github.com/ Megvii-BaseDetection/YOLOX)

## 先行研究と比べて何がすごいか？
- 当時の最新のYOLO(v4, v5)にアンカーフリー検出器を取り入れた

## 技術や手法の肝は？
### 実装の詳細
- YOLOXも提案モデルもハイパーパラメータ等の設定は同じ

### ベースラインモデル
- YOLOv3に以下の改良を加えてCOCOのAPが38.5まで精度を改善したものをベンチマークとして使用
    
#### 分離head
分類タスクと回帰タスクが衝突し精度が下がる問題が知られているが、これまでのYOLOシリーズや特徴ピラミッド(FPN, PANなど)では2種類の検出ヘッドが結合されている。
結合された検出ヘッドが性能を損なう可能性があることを実験により明らかにした
![Alt text](yolox_fig/image-2.png)

1. 分離headにすると収束が早くなる

![Alt text](yolox_fig/image-3.png)

2. YOLOのE2E版では分離headが不可欠。実際に通常のYOLOと分離head版のYOLOを比較すると、後者の方が精度高い

![Alt text](yolox_fig/image-4.png)

#### より強いデータAugment
YOLOv3にMosaicとMixUpを追加（これ自体は元からある手法）。これにより、AP42%に改善した。
![Alt text](yolox_fig/image8.png)
![Alt text](yolox_fig/image9.png)

#### アンカーフリー
YOLOv4, v5はYOLOv3のアンカーベースの手法を採用しているが、これには以下の問題がある
- 良い感じのアンカー設定をしないといけないし、どんな設定が良いかはドメイン固有なので一般化されていない
- アンカー設定次第で計算量が変わる。エッジデバイスで使う場合とかだとここがボトルネックになることがある

そこで、アンカーフリーの検出器を採用。これにより、42.9%APに改善した。
- アンカー経由せず矩形の左上座標・幅・高さを出力する
- 各物体の中心位置を正事例として割り当てる

#### Multi Positive
上記のアンカーフリーの結果はYOLOv3に合わせるために、教師の中心位置に対応する1点のみを正事例として割り当てていた。これだと、正事例・負事例の不均衡が生じるので、教師の中心に近い3*3個を正事例とする。これにより45%APに改善

#### SimOTA
複数の物体が隣接していてオクルージョンが生じている時、教師と推論の割当に混乱が生じることがある。そこで、割当アルゴリズムを改善
先行研究で、割当を最適輸送問題として考えるOTAという手法があるが、これだと訓練時間が25%増えて余計なハイパーパラメータ必要になる。そこで、これを簡略化したSimOTAを提案。これにより47.3%APに改善

Lijはi番目の教師とj番目の推論結果の損失、λはハイパーパラメータ、clsとregは分類と回帰

![Alt text](yolox_fig/image10.png)

全て1対1に割り当てるのではなく、コストが小さい組み合わせtop kを選んでPositive, それ以外をNegativeとする
kは固定値ではなくGTのサイズや教師同士のオクルージョンを考慮して調整(Dynamic k Estimationという手法を使う)

#### End-to-End YOLO
NMSなしで似たようなことが出来る先行研究の手法を試したが、精度が落ちたので最終的なモデルには使わない

## どうやって有効だと検証した？
### ベンチマークモデルとの比較
いろんなYOLOバックボーンでYOLOXを試したところ、精度が向上した。

![Alt text](yolox_fig/image-5.png)

モバイル機器向けにモデルサイズ小さくしたやつ(Nano)。大幅な軽量化を実現してAPも高い

![Alt text](yolox_fig/image-6.png)

モデルサイズが変わると適切なAugment法も変わる。小さいモデルでは弱めのAugment, 大きいモデルでは強めのAugmentが良い結果。

![Alt text](yolox_fig/image-7.png)

### SOTAとの比較


![Alt text](yolox_fig/image-1.png)


## 議論はある？
従来の手法ではなぜアンカーを導入していたのか気になった

## 次に読むべき論文
- YOLOv6: https://arxiv.org/abs/2209.02976
- YOLOv7: https://openaccess.thecvf.com/content/CVPR2023/papers/Wang_YOLOv7_Trainable_Bag-of-Freebies_Sets_New_State-of-the-Art_for_Real-Time_Object_Detectors_CVPR_2023_paper.pdf
- YOLOv8: https://docs.ultralytics.com/ (論文じゃないけど)
- OTAの論文: https://arxiv.org/abs/2103.14259
