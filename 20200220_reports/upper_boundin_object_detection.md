Empirical Upper Bound in Object Detection and More
===

Ali Borji, Seyed Mehdi Iranmanesh

https://arxiv.org/abs/1911.12451v3

@cohama


## どんなもの?

- よく使われる物体検出のデータセット (PASCAL VOC, MS COCO, OpenImages, あと、独自データセットのFASHION) について精度の上限を求めた
  - 91.6 (VOC), 78.2 (COCO)
  - 枠の座標を固定した上で単純に分類機を学習させた
    - 物体らしさの検出と枠の回帰が精度100%の想定
- 現状モデルの詳細なエラー分析をした
  - 背景から誤認識することが多い

## 先行研究と比べて何がすごい？

- 物体検出の COCO や OpenImage に対してのエラー分析はなかった

## どうやって有効だと検証した？

- 教師の枠を切り抜いた画像で分類機を訓練 (ResNet152)
  - 枠ぴったりが一番よいことも部分的な実験で確認
- 枠を少しずらした画像でも訓練
  - IOU を下げた状態の想定

## 議論はある?

- 物体らしさの検出が難しそうなので割と順当。
- アノテーションの間違いみたいなものとかは？
- オブジェクト数との関連は？
- クラス別で見ると既存モデルが上限突破しているがそれは。
  - 単純に分類器がしょぼいだけ？

## 次に読むべき論文
Derek Hoiem, Yodsawalai Chodpathumwan, and QieyunDai. Diagnosing error in object detectors. InEuropean con-ference on computer vision, pages 340–353. Springer, 2012.
