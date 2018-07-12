Synthesizing Audio with Generative Adversarial Networks
===

[arxiv](https://arxiv.org/abs/1802.04208)
[github](https://github.com/chrisdonahue/wavegan)


@hissanova


## どんなもの?

音を生成する GAN

## 技術や手法の肝は？

FFT を用いず、直接波形を生成している.
既存の FFT などの手法は音の位相の情報が失われるが、波形を直接生成するので、その損失がない。

## どうやって有効だと検証した？

実際に作った音が人間が好んだ（原文アブストラクト）

## 先行研究と比べて何がすごい？

スペクトル分解を使わず、生の音のデータを直接学習しているところ

## 次に読むべき論文

未定です、、、
