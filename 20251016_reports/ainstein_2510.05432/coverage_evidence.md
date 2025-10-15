# ページ網羅性チェック
| PDFページ | 主な記載 | 要約・画像での反映 |
| --- | --- | --- |
| 1 | タイトル、著者、アブストラクト概要 | 「著者」節および「# どんなもの？」全体で全体像を要約 |
| 2 | 研究の動機・研究課題、データセット構成、概念的活性化エネルギー | 「# どんなもの？」1 行目・4 行目、「# 議論はある？」3 行目で引用 |
| 3 | 関連研究の整理 | 「# 先行研究と比べてどこがすごい？」各箇条書き |
| 4 | 方法論（Algorithm 1、内部/外部批評ループ） | 「# 技術や手法の肝は？」および `pipeline_overview.png` |
| 5 | 評価指標定義、埋め込み・可読性計測、ELO 概要 | 「# 技術や手法の肝は？」後半、「# どうやって有効だと検証した？」1・5 行目、`performance_metrics.png` |
| 6 | Table 3（τ=4/5 比較）、Mi の優位性、Rediscovery と Novel & Valid の挙動 | 「# どうやって有効だと検証した？」2〜4 行目、「# 議論はある？」1〜2 行目、`performance_metrics.png` |
| 7 | 図3（ティア別性能）、ジャッジ置換の頑健性 | 「# どうやって有効だと検証した？」4 行目、「# 議論はある？」1 行目 |
| 8 | Table 5（Human-verified ELO）、ケーススタディ | 「# どうやって有効だと検証した？」5 行目で参照 |
| 9 | Table 6（コサイン類似度・可読性）、クラスタリング概要 | 「# 技術や手法の肝は？」5 行目、「# どうやって有効だと検証した？」6 行目、`solution_clusters.png` |
| 10 | 結論（Mi 依存、再発見と創造性の洞察） | 「# 議論はある？」全体、および「## 私見」冒頭 |
| 11 | 参考文献 | 参考情報（本文要約では直接引用せず） |
| 12 | 付録B：統計的有意性検定 | 参考情報（今回の要約では詳細割愛） |
| 13 | 付録C：Human ELO 追加ケース | 「# どうやって有効だと検証した？」5 行目で ELO の人手検証に言及 |
| 14 | 付録C/D：追加ケーススタディ・クラスタ詳細 | 「# 議論はある？」4 行目、`solution_clusters.png` |
| 15 | 付録D：クラスタ分析の詳細 (11 archetypes) | 「# どうやって有効だと検証した？」6 行目、`solution_clusters.png` |
| 16 | 付録D：代表ソリューション例 | 「# どうやって有効だと検証した？」6 行目 |
| 17 | 付録E：プロンプト（Generalizer） | 参考情報（要約外） |
| 18 | 付録E：プロンプト（Solver/Critic） | 参考情報（要約外） |

# 根拠チェック
## どんなもの？
- 「ICLR 2025 採択論文 1,214 本…評価基盤 AINSTEIN」 (p.2)
  > "We curate a dataset of 1,214 high-quality ICLR 2025 papers, stratified by quality tier (Oral, Spotlight, Poster)." (p.2)
- 「Generalizer と Solver の 2 段構成と批評ループ」 (p.4)
  > "Algorithm 1 The AInstein Algorithm ... External model M_e ... Z_final ← SolveWithRefinement(P_final, M_i, M_e)." (p.4)
- 「Success Rate・Rediscovery・Novel & Valid の 3 指標」 (p.5)
  > "Rediscovery: Does a successful solution match the original human solution? (3) Novel & Valid: Is a successful solution valid but different from the original?" (p.5)

## 先行研究と比べてどこがすごい？
- 外部検索や微調整を排除して推論のみを検証 (p.1)
  > "We introduceAInstein, a framework for testing whether LLMs can generate valid solutions to AI research problems using only their pretrained parametric knowledge—without domain-specific fine-tuning, retrieval augmentation, or other external aids." (p.1)
- 欠損スコア d による Generalizer 管理 (p.5)
  > "The deficit score (d) is strongly correlated with these key quality dimensions." (p.5)
- 多面的評価（LLM judge + human + embeddings） (p.5, p.8)
  > "We also assess textual complexity using standard readability scores (e.g., Flesch-Kincaid Grade Level)." (p.5)
  > "Table 5: ELO ratings derived from a head-to-head tournament where human evaluators provided pairwise preferences between solutions." (p.8)

## 技術や手法の肝は？
- 内部/外部批評ループの仕様 (p.4)
  > "Internal Critique Loop ... External Critique Loop (Model M_e): The outer loop provides a higher-fidelity review ..." (p.4)
- 欠損スコア d≈2.5/3.5 の比較 (p.5)
  > "As shown in Table 2, both Qwen-235B and GPT-OSS-120B produce problem statements with very low deficit scores (d ≈ 2.5), while Mistral-24B’s are ... d ≈ 3.5." (p.5)
- 可読性・埋め込みの指標 (p.9)
  > "Table 6: Semantic distance and readability metrics ... Cosine Sim. ↑ ... Flesch Grade ↓." (p.9)

## どうやって有効だと検証した？
- 32,778 試行（3×3×3 組合せ） (p.2, p.6)
  > "We curate a dataset of 1,214 high-quality ICLR 2025 papers..." (p.2)
  > "Table 3: LLM-as-a-judge success rates (%) comparing lenient (τ=4) and strict (τ=5) evaluation thresholds." — 行列が Generalizer × Internal × External (=3×3×3) を網羅 (p.6)
- τ=4/5 での成功率・再発見率の差 (p.6)
  > "Under the relaxed threshold ... 83.77 ... However, when tightening ... these scores plummet to 15-20%." (p.6)
- Novel & Valid の高水準維持 (p.6)
  > Table 3 shows Novel & Valid = 59.39 (τ=5) for GPT-OSS-120B internal model (p.6).
- Human-in-the-loop ELO 検証 (p.8)
  > "Table 5: ELO ratings derived from a head-to-head tournament where human evaluators provided pairwise preferences..." (p.8)
- クラスタリングと 11 アーキタイプ (p.9, p.15)
  > "We first grouped all solutions into semantically coherent clusters via KMeans++ ... This process reveals a rich taxonomy of 11 distinct solution archetypes." (p.9, p.15)

## 議論はある？
- 内部批評モデルが支配的 (p.6)
  > "When solving problems ... the GPT-OSS-120B internal agent achieves a Success Rate of 74.05% ... whereas ... Qwen-235B reaches only 43.82%." (p.6)
- 再発見率が低下し Novel & Valid は安定 (p.6)
  > "Under the relaxed threshold ... rediscovery ... 75-84% ... when tightening ... 15-20%. In contrast, the Novel & Valid metric ... remains high and remarkably stable." (p.6)
- 概念的活性化エネルギー (p.2)
  > "Our concept of 'conceptual activation energy' provides a complementary perspective, focusing on the minimum prompt complexity required to trigger specific reasoning capabilities." (p.2)

## 私見
- Novel & Valid が高い点への言及 (p.6)
  > Table 3 values >60% for Novel & Valid with GPT-OSS-120B internal models (p.6).
- 内部批評強化の重要性 (p.6)
  > Same passage highlights Mi dominance (p.6).

## 画像ごとの根拠
- `figure1_pipeline.png`: Figure 1 のパイプライン図 (p.2).
  > "Figure 1: The AINSTEIN framework. An input scientific abstract (A)..." (キャプション, p.2)
- `figure2_table3.png`: Table 3 の τ=4/5 成績比較 (p.6).
  > "Table 3: LLM-as-a-judge success rates (%) comparing lenient (τ = 4) and strict (τ = 5) evaluation thresholds." (p.6)
- `figure3_clusters.png`: Figure 4 のクラスタ可視化 (p.9).
  > "Figure 4: Visual analysis of the 11 identified research clusters..." (キャプション, p.9)
