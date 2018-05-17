Enhance word representation for out-of-vocabulary on Ubuntu dialogue corpus
===

2018/02/07 Jianxiong Dong(AT&T), Jim Huang(AT&T)

[https://arxiv.org/abs/1802.02614v1](https://arxiv.org/abs/1802.02614v1)

（まとめ：@nharu1san）

---

## どんなもの？
学習していない語彙外の単語に弱い既存手法を、一般的なコーパスとタスク用のコーパスを独自のアルゴリズムで組み合わせて保持することで改善する。

---

## 先行研究と比べて何がすごい？
タスクから作成する単語ベクトルだけでなく、一般的なコーパスも取り入れた所。

---

## どうやって有効だと検証した？
- Ubuntu dialog corpus
- Douban conversation corpus
これらの結果がいずれもSMN(Wu et al., 2017)や素のESIMの正解率を上回った。

---

## 技術や手法の肝は？
ベースのモデルにはEnhanced LSTM(ESIM) (Chen et.,al 2017)を用いており、これに著者らの独自の語彙生成アルゴリズムを用いる。

![図1](https://i.imgur.com/MSOHImm.png)

予めword2vecなどで学習した単語ベクトルとトレーニングセットから生成した単語ベクトルを使い、どちらかにしか存在しない単語は他方をゼロベクトルとして連結、両方に存在する場合はそのまま連結するという作業を繰り返して新しい単語ベクトルを作成する。

![アルゴリズム1](https://i.imgur.com/en1Ic1G.png)

---

## 議論はある？
- Discussion節なし
- (所感) 今回のpre-trainedの単語ベクトルは[https://nlp.stanford.edu/projects/glove/](https://nlp.stanford.edu/projects/glove/)内のCommon Crawl(42B tokens, 1.9M vocab, uncased, 300d vectors)が利用されているが、他のデータを使用した場合や次元数・語彙数の違いによってどのような結果になるか調査されていないのが少し残念。

---

## 次に読むべき論文は？
- [Enhanced LSTM for Natural Language Inference](https://arxiv.org/abs/1609.06038)
  - 今回の著者らがベースとしているESIMについての論文
