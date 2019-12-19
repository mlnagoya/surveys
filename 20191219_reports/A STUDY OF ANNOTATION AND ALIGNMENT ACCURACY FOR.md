Challenges in Search on Streaming Services: Netflix Case Study
===

2019/03/11 Sudarshan Lamkhede, Sudeep Das

https://arxiv.org/abs/1903.04638

（まとめ：yuji38kwmt）

---

## どんなもの？
Netflixなどのストリーミング検索サービスを構築する上での課題を挙げている
* recomendation
* Instant Search


---

## どうやって有効だと検証した？
なし

---

## 技術や手法の肝は？

### Search Usecase
1. Fetch
2. Find
3. Explore

### Recomendation
* 意味のあるrecomentationを提供するための課題
    * What are good recommendations for a search?
    * How to blend the recommendations with search results?
* Unavailable Entities
    * 法律やビジネス要件で閲覧できない動画？
### Instance Search
* Netflixでは、文字数の入力を減らすため、キーストロークでのInstance Searchを提供している
* NetflixはTVで使うことが多い
    * TV UIは入力が難しいからクエリ長が短く、Web UIは入力が簡単だからクエリ長が長くなる
* 韓国語など英語以外だと、文字数よりキーストロークが増える場合がある

![](yuji38kwmt/table1.png)

### GLOBAL AUDIENCE AND CONTENT
* Netflixでは約60%がアメリカ以外
* 


---

## 議論はある？
なし
+ Discussion 節があれば読んだ内容を書く。
+ なくても議論してそうな記述が他にあれば書く。
+ リストで2～4項目程度
    + サブリスト組み合わせてもOK

---

## 先行研究と比べて何がすごい？
なし

---

## 次に読むべき論文は？
なし




--------
### 所感
* 課題に対しての解決方法は載っていない。。。

