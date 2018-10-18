# Born Again Neural Networks
2017 NIPS workshop  Tommaso Furlanello, Zachary C. Lipton, Michael Tschannen, Laurent Itti, Anima Anandkumar

[Born Again Neural Networks](http://export.arxiv.org/pdf/1805.04770)

## どんなもの？
これまで，Knowledge Distillation（蒸留）はモデルの軽量化を図るための手段として扱われてきた．
提案手法であるBANs（Born Again Networks）はKnowledge Distillation（蒸留）をモデルの精度向上を図る手段として用いる．
具体的には，teacher modelと呼ばれる教師モデルの知識をstudent modelと呼ばれる生徒モデルに継承することで，教師モデルの精度を凌ぐ生徒モデルの生成に成功した．

## どうやって有効だと検証した？
実験に使用したデータセット：CIFAR-10/100（画像データ），PTB（Penn Tree Bank）（英語コーパス）
### CIFAR-10/100に関する実験
■BANの精度に関する検証
使用したモデル
- teacher model：DenseNet，student model：DenseNet
→teacher modelとstudent modelが同等のモデルであるときの検証
- teacher model：DenseNet，student model：ResNet
→teacher modelが大規模モデルでstudent modelが小規模モデルであるときの検証
- teacher model：DenseNet，student model：WideResNet or bottleneck-ResNet
→teacher modelが大規模モデルでstudent modelが中規模モデルであるときの検証

■Dark Knowledgeが提案手法に及ぼす効果に関する検証
2種類の実験を行い，効果を検証
- CWTM（Confidence-Weighted by Teacher Max）
→Dark Knowledge内の値を全て0にしてstudent modelの学習を行う
- DKPP（Dark Knowledge with Permuted Predictions）
→Dark Knowledge内の値をシャッフルしてstudent modelの学習を行う

### PTBに関する実験
■BANの精度に関する検証
使用したモデル
- a single layer LSTM
→ユニット数が1500のモデル
- CNN-LSTM
→畳み込み層とハイウェイ層と2層のLSTMを組み合わせたもので，上のモデルよりも小さい

## 技術や手法の肝は？
### Knowledge Distillation
■Knowledge Distillationの流れ
1. teacher model（大規模なモデル）の学習を行う
2. teacher modelのsoft target（出力層の手前のsoftmax関数の出力）とhard target（出力）を用いてstudent modelの学習を行う

### BAN
■BANsの流れ
1. teacher modelを学習
2. teacher modelを元に1番目のstudent modelを学習
3. 1番目のstudent modelを元に2番目のstudent modelを学習
4. これをk番目まで繰り返すことでk個のstudent modelを得る
5. k個のstudent modelをアンサンブルすることでBANsを構築

### Dark Knowledge
■Dark Knowledgeとは
画像認識のタスクでは，neural networkの出力はsoftmax関数から出力される確率分布を元に一番高い確率を示したクラスを1，その他のクラスを0とすることでone-hotベクトルで表す．
Dark Knowledgeとは普段あまり重要視されないsoftmax関数から出力される確率分布（正解クラスの確率を除いた）のことを指す．
これまでの研究では，Dark Knowldegeが蒸留時に大きな影響を及ぼすとされてきたため本論文ではその真偽を検証する．

## 議論はある？
- 本論文では小規模なモデルとしてResNetが紹介されているが，さらに小規模なモデルをstudent modelとして適用可能か？
- 本論文で想定しているモデルはneural networkだが他の手法（例えば決定木）にも適用可能か？
- teacher modelが強すぎるとstudent modelはteacher modelの精度を越えることができない

## 先行研究と比べて何がすごい？
- これまでモデルの軽量化の手段として扱われてきたDistillation Knowledgeをモデルの精度向上のための手段として用いた
- student modelを再帰的に蒸留し，これらの過程で得られた全てのstudent modelをアンサンブルすることでteacher modelの精度を遥かに凌ぐstudent modelの
生成に成功した

## 次に読むべき論文は？
[A gift from knowledge distillation: Fast optimization, network minimization and transfer learning](http://openaccess.thecvf.com/content_cvpr_2017/papers/Yim_A_Gift_From_CVPR_2017_paper.pdf)
