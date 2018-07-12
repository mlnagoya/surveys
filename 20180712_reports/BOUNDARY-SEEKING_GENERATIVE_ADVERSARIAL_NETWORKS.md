

# BOUNDARY-SEEKING GENERATIVE ADVERSARIAL NETWORKS
[BOUNDARY-SEEKING GENERATIVE ADVERSARIAL NETWORKS](https://arxiv.org/pdf/1702.08431.pdf)


* R Devon Hjelm
* Athul Paul Jacob
* Tong Che
* Adam Trischler
* Kyunghyun Cho
* Yoshua Bengio




# どんなもの？
BGAN(BOUNDARY-SEEKING GAN)という提案。


## 何故読んだ？

被引用数が37と多いので
ICLR2018の論文なのでとりあえず手を付けた


# 先行研究と比べてどこがすごい？
トレーニングアルゴリズムの新提案（BOUNDARY-SEEKING)。
GANでは離散的な分布にはGのパラメータが使えなかった、
離散的変数と連続的変数のどちらにも効果的な単一のフレームワーク。
トレーニングの安定性が向上。


# 技術や手法の肝は？
生成サンプルに対して重み（importance weights）を付加。
重みがDの決定する境界と関係あるのでBGAN(BOUNDARY-SEEKING GAN)と命名。


# どうやって有効だと検証した？
離散的な変数（言語モデル）とイメージデータの2種類を用意
ベースラインとの比較ではそれ程差がない。対象のWGANはいろいろ試したが成績振るわず。





# 次に読むべき論文は？
Arjovsky, Martin, Chintala, Soumith, and Bottou, Leon. Wasserstein gan. ´ arXiv preprint
arXiv:1701.07875, 2017.
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTI1Mzg5NzE4MiwxMjI4NTczOTYxXX0=
-->
