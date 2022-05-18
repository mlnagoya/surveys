
# Visualizing the Loss Landscape of Neural Nets
Author : Hao Li, Zheng Xu, Gavin Taylor, Christoph Studer, Tom Goldstein

所属：メリーランド大学カレッジパーク校、アメリカ合衆国海軍兵学校、コーネル大学

https://arxiv.org/abs/1712.09913 （原著論文）

まとめ：細井博之

## どんなもの？
- 深層学習モデルの損失関数の様子を可視化する
- モデルの訓練が上手く行くor行かないの違いが分かりやすくなる 
![Screenshot from 2022-05-18 14-35-43](https://user-images.githubusercontent.com/1649997/168964675-93fe8b0b-6887-42a1-8132-4200bae980a7.png)


## 先行研究と比べてどこがすごい？
- Filter normalization scheme により ReLU のスケール不変性にも対応した

## 技術や手法の肝は？
### Filter normalization scheme
- ReLU にはスケール不変性がある（重みのスケールがフィルタごとに異なる）
    - Loss Landscape を得るときに、同じように重みの数値を動かしても、動かす重みによって影響度が変わってしまう
    - バッチノーマライゼーションが使われる場合は特に顕著
- そこで先にフィルタ単位で重みを正規化しておいて、これらの影響が出ないようにする
- 畳み込み層だけではなく最終結合層にも適用される
### PCA（主成分分析）
- 大量のパラメータ空間を2次元に落とし込むときに、どの軸を選ぶべきかという問題
- ![Screenshot from 2022-05-18 14-44-57](https://user-images.githubusercontent.com/1649997/168965848-10dc72d1-b489-47be-bfa0-8a0b23d81a5c.png)
- 適当に選ぶと軌跡の垂直方向の意味が掴めなくなってしまう
- PCA（主成分分析）を使って、これらの軸を求める
- ![image](https://user-images.githubusercontent.com/1649997/168966588-f1a9dbd9-c744-4523-b626-fed153216473.png)

## どうやって有効だと検証した？
- 実際に Loss Landscape を出してみて事例を見比べた


- SGDを使った1次元と2次元の可視化。各グラフの下の文字は、weight decay、バッチサイズ、テストデータのエラー。![Screenshot from 2022-05-18 20-28-14](https://user-images.githubusercontent.com/1649997/169028532-283fe69d-96fb-43fc-9392-8e1fbde028a2.png)
<br><br>

- ResNetの各サイズのスキップあり（上段）となし（下段のNS）の比較。![Screenshot from 2022-05-18 20-27-28](https://user-images.githubusercontent.com/1649997/169028458-bf213b38-b1d4-4b6c-afc8-2bd08d7b98f4.png)
<br><br>

- Wide-ResNet-56 で、フィルタサイズ（kの倍数)の比較。上段がスキップあり、下段がスキップなし。![Screenshot from 2022-05-18 20-26-59](https://user-images.githubusercontent.com/1649997/169028352-1ca91d3b-f513-429d-b576-19350ad716ed.png)
<br><br>

- 訓練時の軌跡。各左側がバッチサイズ128、右側がバッチサイズ8192。Weight decay ありでバッチサイズ小さいと、等高線と並行に軌道を描くような動きを示す。赤い点は学習率が下がったことを示す。![Screenshot from 2022-05-18 20-33-08](https://user-images.githubusercontent.com/1649997/169029865-9320629b-85aa-43db-bbfa-1a9637fe03ae.png)
<br><br>

- 1次元で、ランダムな方向に10回分を重ねてみた様子。ランダムにもかかわらずかなり近い傾向を示す。![Screenshot from 2022-05-18 20-37-56](https://user-images.githubusercontent.com/1649997/169030234-aa430a88-6a00-4c17-aae6-349b64395217.png)


## 議論はある？
- データによってどう変わるかにも興味がある。 

## 次に読むべきタイトルは？
- On the loss landscape of a class of deep neural networks with no bad local valleys https://arxiv.org/abs/1809.10749
