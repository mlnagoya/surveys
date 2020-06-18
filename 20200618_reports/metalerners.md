Metalearners for estimating heterogeneous treatment effects using machine learning
===

2018/12/18 
Sören R. Künzel (Department of Statistics, University of California)
Jasjeet S. Sekhon (Department of Statistics, Department of Political Science, University of California)
Peter J. Bickel (Department of Statistics, University of California)
Bin Yu (Department of Statistics, Department of Electrical Engineering and Computer Science, University of California)

https://www.pnas.org/content/116/10/4156

（まとめ：龍一郎 @K_Ryuichirou）

---

## どんなもの？

+ 条件付き平均処置効果 (Conditional Average Treatment Effect) を推定する手法 X-learner を提案する
+ X-learner は処置群と対照群の比が偏っている場合であっても動作することが期待できる
+ 既存の決定木ベースの手法 (Random Forest or Bayesian Additive Regression Trees; BART) よりも良い結果を示した
+ 作成した解説スライド https://speakerdeck.com/asei/overview-of-causalml

---

## どうやって有効だと検証した？

+ 既存のデータセットを用いた検証 (Get-Out-the-Vote)
  + 現実で A/B テストを行った実験、“DO YOUR CIVIC DUTY—VOTE!” というチラシが届く
  + 共変量: 人の様々な属性値 (性別、年齢、過去の選挙で投票に行ったか)
  + 処置群: チラシが近所に届く
  + 対照群: 何もしない
  + アウトカム: 今回の選挙で投票に行ったかどうか
+ RMSE を用いた評価により、既存の手法よりも少ないデータ数でも高精度で推定できることがわかった

---

## 技術や手法の肝は？

+ 2段階で機械学習モデルを用いる
  + 1段階目: control群、treatment 群のデータを用いて、アウトカムを予測するモデルを2つ作る
  + 2段階目の前処理: control群、treatment群、それぞれのデータについて、アップリフトを推論しておく
  + 2段階目: control群、treatment群それぞれのアップリフトを予測するモデルを2つ作る
  + 2段階目で作成した2つのモデルをアンサンブルする
+ データが treatment/control どちらかに偏っている場合でも、データの多い方のモデルを用いて推定できるので結果が安定する

---

## 議論はある？

+ 利用する機械学習モデルによって推論結果が大きく変わる
  + Random Forest を用いるのが良かったとされている
+ 最終的に行うアンサンブルのやり方について、実利用時には自分で決定する必要がある
  + 傾向スコア (control/treatment のどちらに所属しそうか予測するモデルの出力値) を用いればよさそうだとされている

---

## 先行研究と比べて何がすごい？

+ ATEを計算できる他の手法 (IPWや傾向スコアマッチング) では CATE を得るのは用意ではないが、本手法なら推定できる
+ 通常、機械学習勢が考えるアップリフトモデリングである T-learner (詳細は「仕事で始める機械学習」を参照) よりも高い精度で推定できる

---

## 次に読むべき論文は？

+ Quasi-Oracle Estimation of Heterogeneous Treatment Effects https://arxiv.org/abs/1712.04912 (R-learner の提案)
+ Automated versus do-it-yourself methods for causal inference: Lessons learned from a data analysis competition https://arxiv.org/abs/1707.02641 (BARTの提案)
+ An introduction to g methods https://academic.oup.com/ije/article/46/2/756/2760169 (異なる因果推論の手法である g-method の解説)
