#Transfer Learning for Automated Optical Inspection

##転移学習の検査精度はなぜ高いのか~SORAサクライ　櫻井　敏明
===

Submitted on May 2017 
　
https://ieeexplore.ieee.org/document/7966162/
---
　

#どんなもの？

## 背景

* モデル VGG16を使い、DAGM（工業用欠陥画像データセット）によって転移学習の有用性を調査。
* ①ImageNet で VGG16による1000の多値分類。
* ②上記①で得た重み（層1～13）を転移させた学習モデルを構築
* ③最後の結合層（層14～16）のみ12の多値分類としたVGG16で、DAGMのデータ分類の精度を測る。



---

## どうやって有効だと検証した？


* 以下３種類で比較
* Randomly Initialized Network …単純にDAGMデータをVGG16で学習
* Frozen Network　・・・ ImageNet で学習して得た重みを利用。ただし1-13層は重みを固定とする。
* Fine-tuned Network ・・・　ImageNet で学習して得た重みを初期値に、DAGMデータのミニバッチでSGD更新。

---

## 実験の結果
* 1回目のエポックでFine-tuned Network が一気に99.95％の高精度に
* ImageNetとDAGM がいかに異なる画像イメージであるかを説明 

---
## でもなぜ転移学習が有効？

* Fine-tuned でどのような表現(入力)で出力の最大化を引き出すのか？　明確な特徴がない。
* Randomly Initialized Network と比較。下層に近づくほど学習率は結局同じ。
　
---
## でもなぜ転移学習が有効（その２）？
* 最後の結合層の入力で、Frozen Network　に比べてFine-tuned は不要な情報が消されている。
* 下層へ行くほど無駄な情報が消されて情報の希薄性が明確になることがわかった。

---
## 結論

* 転移学習では学習の過程で、不要な情報が消去され、結果的に必要な情報を残してモデルができる。


---

## 次に読むべき論文は？

引き続き、製造現場に関連する転移学習ものを探します。
