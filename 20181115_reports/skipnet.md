SkipNet: Learning Dynamic Routing in Convolutional Networks
====

Xin Wang, Fisher Yu, Zi-Yi Dou, Trevor Darrell, Joseph E. Gonzalez

[paper](http://openaccess.thecvf.com/content_ECCV_2018/html/Xin_Wang_SkipNet_Learning_Dynamic_ECCV_2018_paper.html)

@cohama


## どんなもの?

- 入力に応じて不要な層を動的にスキップするようなネットワークをもつ SkipNet を実装した

## 技術や手法の肝は？

- 普通にやると微分不可能になってしまうところを、教師あり学習と強化学習のハイブリッド手法により解決

## どうやって有効だと検証した？

- CIFAR、ImageNet、SVHN のそれぞれの SOTA モデルと比較
  - SACT, LCCL, PFEC
- 精度を損なわずに 37-80% の FLOPS 減

## 先行研究と比べて何がすごい？

- 疎にするやつ、channel pruning、量子化、蒸留などの手法は Post Processing だが、
  SkipNet はそういう手間はいらない


## 議論はある

- FLOPs で見てるけど実時間は？
- 動的アーキテクチャは今後も重要だよ

## 次に読むべき論文

- lukbasi, T., Wang, J., Dekel, O., Saligrama, V.: Adaptive neural networks for efficient
inference. In: Proceedings of the 34th International Conference on Machine Learning. pp.
527–536 (2017)
- ll, M., Perona, P.: Deciding how to decide: Dynamic routing in artificial neural networks.
In: Proceedings of the 34th International Conference on Machine Learning. pp. 2363–2372
(2017)
- v, M., Collins, M.D., Zhu, Y., Zhang, L., Huang, J., Vetrov, D., Salakhutdinov, R.:
Spatially adaptive computation time for residual networks. In: The IEEE Conference on
computer Vision and Pattern Recognition (July 2017)
