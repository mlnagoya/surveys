# A SURVEY ON CONTRASTIVE SELF-SUPERVISED LEARNING
https://arxiv.org/abs/2011.00362v3

(まとめ @ma)

著者
* Ashish Jaiswal
* Ashwin Ramesh Babu
* Mohammad Zaki Zadeh
* Debapriya Banerjee
* Fillia Makedon

The University of Texas at Arlington

# どんなもの？
自己教師学習（対比学習）の要約

ComuterVisionがメイン、NLPも

# 先行研究と比べてどこがすごい？
全体像つかめる、アーキテクチャーの経緯がわかる

# 技術や手法の肝は？

対比学習概要



![image-20210616211902454](contrasive_2011.00362/image-20210616211902454.png)

![image-20210617182132114](contrasive_2011.00362/image-20210617182132114.png)





４つのアーキテクチャーの説明


![](\contrasive_2011.00362/image-20210615065515442.png)

![image-20210615065647377](contrasive_2011.00362/image-20210615065647377.png)

![![image-20210615065734591](contrasive_2011.00362/image-20210615065734591.png)



# どうやって有効だと検証した？

## データセット　ImageNet
![image-20210615065355109](contrasive_2011.00362/image-20210615065355109.png)

![image-20210615065816930](contrasive_2011.00362/image-20210615065816930.png)

注意領域が広がっている？

![image-20210615065853434](contrasive_2011.00362/image-20210615065853434.png)

![image-20210615065943573](contrasive_2011.00362/image-20210615065943573.png)




# 議論はある？


## 私見
去年位まで、教師あり学習（データ＋ラベル）が意味ある予測には当然と思ってましたが、自己教師あり＋（ラベル）が普通になるのかなと思ってるので、この領域の発展目が離せない。

SwAVが取り入れたデータ拡張のやり方がほかのアーキテクチャーでも結構効いている。データ拡張新しい主張だけの論文とかでてくるか気になる。

# 次に読むべき論文は？
* [Unsupervised Learning of Visual Features by Contrasting Cluster Assignments](https://arxiv.org/abs/2006.09882)

  SwAVの仕組みがよくわからないので

