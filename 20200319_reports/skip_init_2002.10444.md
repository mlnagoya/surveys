# Batch Normalization Biases Deep Residual Networks Towards Shallow Paths
[https://arxiv.org/abs/2002.10444](https://arxiv.org/abs/2002.10444)
(まとめ @n-kats)

著者
* Soham De
* Samuel L. Smith

（DeepMind）

# どんなもの？
BatchNormalization無しで訓練する方法としてSkipInitを提案

![](skip_init_2002.10444/skip_init.png)


# 先行研究と比べてどこがすごい？
* BatchNormalizationは小さいバッチサイズで上手く機能しない
* Fixupは層の深さによって初期値のスケールをコントロールする手法（設定が面倒くさい）

SkipInitはFixupと同じモチベーションながら、設定が簡単

![](skip_init_2002.10444/compare_to_bn.png)

# 技術や手法の肝は？




# 議論はある？
# 次に読むべき論文は？
