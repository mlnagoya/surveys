Sequential Matching Network: A New Architecture for Multi-turn Response Selection in Retrieval-based Chatbots
===

2016/12/06 Yu Wu(Beihang University), Wei Wu(Microsoft Research), Chen Xing(Nankai University), Zhoujun Li(Beihang University), Ming Zhou(Microsoft Research)

[https://arxiv.org/abs/1612.01627](https://arxiv.org/abs/1612.01627)

（まとめ：@nharu1san）

---
## どんなもの？
チャットボットにおいて、複数のやりとりをする際に文脈情報や発話関係をできるだけ失わずに会話させるネットワーク構成を提案する

---
## どうやって有効だと検証した？
- Theanoで実装し、Ubuntu CorpusおよびDouban Conversation Corpusについてテストを行い、他の手法(TF-IDF, RNN, CNN, LSTM, BiLSTM, Multi-View, DL2R, MV-LSTM, Match-LSTM, Attentive-LSTM)と比較した。
  - Ubuntuコーパスでは既存手法に比べて6%以上、Douban Conversation Corpusでは3%の有意な改善が見られた。
- また、SMN内の構成を部分的に置き換えた結果から発話間の関係やM1・M2による類似度の有用性を示した。
---

## 技術や手法の肝は？
### SMN (Sequential Matching Network)
GRUとCNNを組み合わせた三層から成るネットワーク。発話群(u1...un)と応答文(r)を入力し、現在の会話状態にその応答が適切であるかスコアリングする

#### 第一層 Utterance-Response Matching
単語分散表現を入力とし、UtteranceとResponse間の単語類似度をM1、GRUから作成したシークエンス類似度をM2としてCNNへ入力する

#### 第二層 Matching Accumulation
n個の発話ベクトルをさらにGRUへと入力、発話の依存関係や類似度の累積を貯える

#### 第三層 Matching Prediction
三通りの出力方法を定める

- SMN(latest): 最後の値を出力する
- SMN(static): 入力それぞれに重みを掛けて足し合わせる
- SMN(dynamic): 一致ベクトルと発話ベクトルから動的に計算する

---

## 議論はある？
- 論理的一貫性を考慮しない
  - 文脈は合っているものの、論理的でない回答のスコアが高くなる
- 検索後に正しい候補がない場合がある

---

## 先行研究と比べて何がすごい？
- 発話それぞれを応答文と一致させる
- GRUによって(発話と応答文の)一致情報を蓄積する

有用な一致情報が十分に保持される点で優れる

---

## 次に読むべき論文は？
- [A Sequential Matching Framework for Multi-turn Response Selection in Retrieval-based Chatbots](https://arxiv.org/abs/1710.11344)
  - Wuらのより新しい論文
  - 論文中ではsequential convolutional network(SCN)という名前でSMNが比較されている
- [Improving Retrieval Modeling Using Cross Convolution Networks And Multi Frequency Word Embedding](https://arxiv.org/abs/1802.05373)
  - Wuらのモデル(SMN)よりも良い結果を得られたとするモデル
  - LSTMとCNNを組み合わせている
