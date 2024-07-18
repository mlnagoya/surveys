"驚くほどキレイな三次元シーン復元、「3D Gaussian Splatting」を徹底的に解説する"
を解説する
===

最終更新日 2024年06月10日
投稿日 2024年05月20日
Author:Liu Yang　@scomup
Organization:[パナソニックアドバンスドテクノロジー](https://qiita.com/organizations/panasonic_ad)


URL：https://qiita.com/scomup/items/d5790da25a846e645de1
GitHub：https://github.com/scomup/EasyGaussianSplatting


(まとめ：Hisashi Takagi）

---

## どんなもの？

+ 「3D Gaussian Splatting」という技術を用いて、少数の写真から高精度で美しい3Dシーンを復元する
+ 従来のメッシュや点群を使用した手法よりも表現力が高く、自然な光の反射や色彩の変化を再現することが可能
+ ただし、この記事は学習済みの3D Gaussianを使用して2D画像を生成する手法について解説。学習方法については説明していない（別途解説する予定）


## 背景

+ 3Dオブジェクトを表現する一般的な方法には、メッシュ（三角形の集合体）や点群、ボクセル（空間を小さな立方体に分割）がある
+ しかし、これらの方法は高精度な描画には限界がある
+ 「3D Gaussian Splatting」は、NDT（Normal Distribution Transform）に似た方法で、ボクセルではなく3Dガウス分布を用いてオブジェクトを表現

+ ※NDT（Normal Distribution Transform）とは？　環境や物体の3Dスキャンデータを統計的にモデリングし、空間の特徴を正規分布で表現する技術

---

## どうやって有効だと検証した？

+ この手法により、非常に詳細で自然な3Dシーンの復元が可能になり、特に視点の移動に伴う光の反射や色の変化がリアルに再現される
+ 実際のデモ　[3D Gaussian Splatting + Insta360 RS 1" - Waterlily House, Kew Gardens](https://www.youtube.com/watch?v=mD0oBE9LJTQ&t=5s)

---

## 技術や手法の肝は？


+ この技術は、3Dガウス分布の中心点と共分散行列を用いて、オブジェクトの形状と色を表現します。以下の手順で3Dシーンを2D画像に変換します
  + 3Dガウスの中心点を2D画面に投影
  + 3D共分散行列を計算
  + カメラの視点に応じて2D共分散行列を導出
  + 視点方向に依存する色情報を計算
  + 以上の情報を用いて2D画像を生成する


+ ゲームや映画のCG制作、仮想現実（VR）などでの応用

---

## 議論はある？


+ ガウス分布のパラメータ設定や計算コストが高く、リアルタイム処理には向いていない
+ 複雑なシーンでは大量の計算資源が必要


---

## 先行研究と比べて何がすごい？

+ 「3D Gaussian Splatting」は高密度なガウス分布を使用することで、より細かいディテールを表現することができる
+ 色の変化や反射のシミュレーションも可能


---

## 次に読むべき論文は？


+ [3D Gaussian Splatting for Real-Time Radiance Field Rendering ](https://arxiv.org/abs/2308.04079)
  
+ [Awesome 3D Gaussian Splatting Resources](https://github.com/MrNeRF/awesome-3D-gaussian-splatting)
 


