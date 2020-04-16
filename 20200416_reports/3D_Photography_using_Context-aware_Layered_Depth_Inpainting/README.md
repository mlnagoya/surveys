
3D Photography using Context-aware Layered Depth Inpainting
===

[https://drive.google.com/file/d/17ki_YAL1k5CaHHP3pIBFWvw-ztF4CCPP/view](https://drive.google.com/file/d/17ki_YAL1k5CaHHP3pIBFWvw-ztF4CCPP/view)

(まとめ @crnrbt)



- 著者
  - Meng-Li Shih *1 *2
  - Shih-Yang Su *1
  - Johannes Kopf *3
  - Jia-Bin Huang *1
- 所属
  1. Virginia Tech
  2. National Tsing Hua University
  3. Facebook

---

## どんなもの？

+ 1枚のRGB-D画像をもとに、前景によって隠れている背景を高品質に補完しながら、3D画像(Layered Depth Image)を生成する手法
![Sample1](https://github.com/strshp/surveys/blob/20200416/20200416_reports/3D_Photography_using_Context-aware_Layered_Depth_Inpainting/sample1.png)
![Sample2](https://github.com/strshp/surveys/blob/20200416/20200416_reports/3D_Photography_using_Context-aware_Layered_Depth_Inpainting/sample2.png)

## 先行研究と比べて何がすごい？

+ 1枚のRGB-D画像のみを使用するため、適用範囲が広い。(CNNでDepthを推定することで、RGB画像にも適用可能)
+ コンテキストを意識した補完を行うことにより、オクルージョンが発生している部分についても自然な見た目を実現できる
+ オクルージョンが発生している部分の補完を行う際、色情報だけでなく、深度情報の補完も行う
+ リストで2～4項目程度
  + サブリスト組み合わせてもOK

---

## どうやって有効だと検証した？

+ Experiments で読んだ内容を書く。
+ リストで2～4項目程度
    + サブリスト組み合わせてもOK

---

## 技術や手法の肝は？

+ 3D画像表現として、LDIを利用する
    + 
+ リストで2～4項目程度
    + サブリスト組み合わせてもOK

---

## 議論はある？

+ Discussion 節があれば読んだ内容を書く。
+ なくても議論してそうな記述が他にあれば書く。
+ リストで2～4項目程度
    + サブリスト組み合わせてもOK

---

+ + 

---

## 次に読むべき論文は？

+ Reference の他の論文で読んだ方が良さげなものをピックアップ
+ [Web で公開されている論文ならリンクにする](https://arxiv.org/pdf/1710.05941.pdf)
    + サブリストでそれがどんな論文か一言あるとBetter
