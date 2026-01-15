# coverage_evidence

対象: Higher-Order Knowledge Representations for Agentic Scientific Reasoning (arXiv:2601.04878)

## 準備メモ
- PDFをローカルに保存してページ数を確認する（後述コマンド）。
- 各ページの主題を1〜2行で書き、要約本文のどこに反映したか（章・箇条書き）を対応付ける。
- 図表は「どの主張の根拠か」をページ番号付きでメモする（画像切り出し時のファイル名決めに使う）。

## PDF取得
- URL: https://arxiv.org/pdf/2601.04878
- ローカルパス: `/home/assistant/.cache/papers/2601.04878.pdf`
- ページ数: 34

ページ数確認（例）:
- `python3 -m venv .venv && . .venv/bin/activate && pip install -U pip pypdf`
- `python3 - << 'PY'\nfrom pypdf import PdfReader\nr=PdfReader('/home/assistant/.cache/papers/2601.04878.pdf')\nprint(len(r.pages))\nPY`

## ページ対応表
TODO: 通読後に詳細化する（まずは粗い当たり）

| Page | 主要トピック | 要約への反映先 | 図表/根拠メモ |
| --- | --- | --- | --- |
| 1 | Abstract/Intro（hypergraphでhigher-order関係を保持、agentic traversal、teacherless guardrail） | `20260115_reports/higher_order_knowledge_2601.04878.md` の `# どんなもの？` | 要旨内の数値（≈1,100 papers / 161,172 nodes / 320,201 hyperedges / exponent ≈ 1.23） |
| 2-9 | 先行研究/graph vs hypergraphの定義、pairwise投影の限界 | `# 先行研究と比べてどこがすごい？` | Figure 4（graph projection vs hypergraphの図）候補 |
| 10-12 | hypergraph構築パイプライン（chunking、二段抽出、event→hyperedge） | `# 技術や手法の肝は？` | Algorithm 1 周辺（図/表があれば切り出し） |
| 13-19 | biocomposite scaffold hypergraphの解析（ハブ、構造中心性など） | `# どうやって有効だと検証した？` | Table 1（構造特性のまとめ）候補 |
| 20-25 | Agentic Reasoning（GraphAgent/Engineer/Hypothesizer、IS/K、ケーススタディ） | `# 技術や手法の肝は？` / `# どうやって有効だと検証した？` | Figure 8-12（対話ログ＋システム図）候補 |
| 26 | Conclusion（teacherless frameworkの位置づけ） | `# 議論はある？` | conclusion段落の主張 |
| 27-28 | Methods（AutoGen、embedding、traversal詳細） | `# 技術や手法の肝は？` | traversal（BFS/IS/K）の文章根拠 |
