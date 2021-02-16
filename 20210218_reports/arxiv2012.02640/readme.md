A Comparison of Natural Language Understanding Platforms for Chatbots in Software Engineering.
===

2020/12/04
Ahmad Abdellatif, Khaled Badran, Diego Elias Costa, Emad Shihab
Senior Member, IEEE

https://arxiv.org/abs/2012.02640

（まとめ：井上嵩浩 as @takinou0）

---

## どんなもの？

+ Abstract/Conclusion/Introduction で読んだ内容を書く。
+ リストで2～4項目程度

+ Abstract
	+ クラウドベンダーなどの提供しているチャットボット用の言語推定エンジンは複数あるが、質疑応答させる分野によって得意・	不得意がある。
	+ 分野毎に検証結果があるが、Software Engineeringの領域では検証がされていないため、検証してみた。
	+ 比較対象は、IBM Watson, Google Dialogflow, Microsoft Luis, オープンソースRasa の4種類。
	+ 製品ごとの精度の良し悪しは、与えるFAQデータ次第だが、F値で考えると、IBM Watsonが最も良かった。

---

## どうやって有効だと検証した？

+ Experiments で読んだ内容を書く。
+ リストで2～4項目程度
    + サブリスト組み合わせてもOK

+ 2種類の質問を用意して、検証を行った。
	+ 実際のシステム開発プロジェクトで使われている質問などのレポジトリ
		+ 例
		+ "List me the changes done in ClassA.java"
		+ "Who has the most bug assignments?"
	+ stack overflow (https://stackoverflow.com) に登録されているQ&Aデータ
		+ 例
		+ "How to create an JS object from scratch using a HTML button?"
		+ ""

---

## 技術や手法の肝は？

+ Experiments/Methods 等で読んだ内容を書く。
+ リストで2～4項目程度
    + サブリスト組み合わせてもOK

+ 精度を比較してみました、だけなので、あまり肝という肝はない。
+ 企業では、ベンダーの作成しているエンジンをそのまま利用することが多いため、調査が既になされているのはありがたい。

---

## 議論はある？

+ Discussion 節があれば読んだ内容を書く。
+ なくても議論してそうな記述が他にあれば書く。
+ リストで2～4項目程度
    + サブリスト組み合わせてもOK

---

## 先行研究と比べて何がすごい？

+ Related Works を読んだ内容を書く。
+ リストで2～4項目程度
    + サブリスト組み合わせてもOK
、
+ 論文曰く、2点ある。
	+ リスト提示や予測など、複数の観点でNLUを比較したところが珍しい。
	+ SE領域に関連したFAQのデータを使っていることが珍しい、とのこと。
	
+ 私見

---

## 次に読むべき論文は？

+ Reference の他の論文で読んだ方が良さげなものをピックアップ
+ [Web で公開されている論文ならリンクにする](https://arxiv.org/pdf/1710.05941.pdf)
    + サブリストでそれがどんな論文か一言あるとBetter
