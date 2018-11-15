Automatic Full Compilation of Julia Programs and ML Models to Cloud TPUs
===

2018/10/23 Keno Fischer, Elliot Saba (Julia Computing, Inc.)

https://arxiv.org/abs/1810.09868

（まとめ：[@antimon2](https://github.com/antimon2)）

---

## どんなもの？

+ Julia から XLA IR を直接生成し TPU 上で実行

---

## どうやって有効だと検証した？

+ VGG19 を実装し、FW/BW で動作確認
    + FW 0.23秒/100枚
    + ↑CPUだと52.4秒/100枚かかる

---

## 技術や手法の肝は？

+ XRT
    + シリアル化された XLA IR を受け入れ低レベルのメモリ管理機能を提供するWebサービス
    + つまり PCIe 経由で直接ではない
+ XLA (Accelerated Linear Algebra) 
    + Google が提供する（多次元？）線型代数コンパイラプロジェクト
+ Julia
    + ダイナミックセマンティクス（動的な多重ディスパッチ等）
    + 静的コンパイラ埋込（対応するLLVM関数へのマッピング等）
        + ↑をLLVMの代わりにXLAにコンパイルのが今回の研究
    + 型推論

---

## 議論はある？

+ 現状は "All or nothing"
    + 部分的にoffloadする/しないに分ける研究必要
+ 分散コンピューティングに未対応（不十分？）
    + Juliaの分散コンピューティングと統合するの面白そう

---

## 先行研究と比べて何がすごい？

+ 《該当なし》

---

## 次に読むべき論文は？

+ [Don't Unroll Adjoint: Differentiating SSA-Form Programsa](https://arxiv.org/abs/1810.07951)
    + コード→コードで algorithmic differentiation する話と Julia による実装
