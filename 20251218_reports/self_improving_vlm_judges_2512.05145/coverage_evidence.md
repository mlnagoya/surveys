# coverage_evidence: Self-Improving VLM Judges Without Human Annotations (2512.05145)

## ページごとの要約と要約文書での扱い

### p.1 イントロ・概要・3ステージフレームワーク
- 内容: VLM judge の重要性、人手 preference への依存とそのコスト、自己合成データのみで三段階（ペア生成→判定→学習）の反復で self-train する枠組み、VL-RewardBench / Multimodal RewardBench 上での 0.38→0.51 などの改善と、大規模モデルとの比較結果のサマリ。
- 要約での扱い: `# どんなもの？` で三段階フレームワークとベンチマーク上の改善・大規模モデルと「十分に競合できる」レベルであることを記述済み。`## 概要` でも 3 ステージ構造を再整理している。

### p.2 貢献ポイントと高レベルな主張
- 内容: 提案の貢献箇条書き（人手・クローズド judge なしで 11B judge を大きく改善、VL-RewardBench で 90B / Claude 3.5 と比較可能、GT なしでもイテレーションでスケールすること、ラベルのない新ドメインへの適用可能性）。
- 要約での扱い: `# どんなもの？` で「人手アノテーション・クローズド judge なし」「大規模モデルと競合」「GT なしでも回る枠組み」を含めて言及。`# 議論はある？` でラベルのない新しい画像ドメインへの応用可能性にも触れている。

### p.3 Related work: LLM/VLM-as-a-judge と synthetic data
- 内容: LLM-as-a-judge の既存研究、VLM 評価モデルの人手ラベル大量収集 or クローズドモデル distillation の流れ、synthetic data による self-improvement（Self-Rewarding LM など）を整理。
- 要約での扱い: `# 先行研究と比べてどこがすごい？` で「従来は人手 or GPT/Claude ラベル」「テキスト LLM では自己生成データで reward model を鍛える流れがあった」「それをマルチモーダル judge に広げた」という対比として反映。`# 次に読むべき論文は？` で Self-Rewarding LM と GPT-4V evaluator, RewardBench 系を列挙。

### p.4〜5 手法: データ記法、open/closed 分割、detail alteration と majority voting、judge データ生成と学習
- 内容: D, D_nv, D_v の定義。オープンエンドタスクでは detail alteration により微妙な誤りを入れたペアを生成し、クローズドエンドタスクでは 16 サンプルからの多数決で preferred / less-preferred を構成。前イテレーション judge に A/B 判定と reasoning をさせ、一致するペアのみ残して M^(k+1) を学習。
- 要約での扱い: `## 用語` と `## 擬似ペア生成` で open/closed の区別と、それぞれのペア生成手順（属性・個数・位置のずらし、多数決で多数派回答 vs ランダム別候補）を記述。`## 判定のふるい分け` と `## 反復学習と自己改善` で judge の役割・一致フィルタ・reasoning 利用・イテレーション更新・停止条件をまとめている。

### p.6 実験セットアップとベースライン・ベンチマーク説明
- 内容: LLaVA-OneVision からの 100k プロンプト構成、VL-RewardBench / Multimodal RewardBench の各次元（general, hallucination, reasoning, safety, VQA など）の説明、Llama-3.2-11B-Vision-Instruct を 5 epoch, LR=1e-5 で fine-tune する実装詳細。
- 要約での扱い: `## ベンチマークと設定` で VL-RewardBench / Multimodal RewardBench と各次元を列挙し、ベースラインとして 11B judge を明示。学習率や epoch 数などの細部はレポートでは省略（必要な読者は原文を参照する前提）。

### p.7 結果: イテレーションごとの改善と次元ごとの伸び方
- 内容: Table 2 による VLRB/MMRB 上の base→iteration 4 のスコア推移（0.383→0.538, 0.499→0.539）、general/hallucination/VQA での大きな改善、reasoning/safety での小さな改善、distribution mismatch の指摘。
- 要約での扱い: `## イテレーションごとの伸び` で VLRB 0.38→0.54, MMRB 0.50→0.54 程度の改善と、general/hallucination/VQA の伸び・reasoning/safety の弱さをまとめて説明。`accuracy_vs_iterations.png` プレースホルダで全体のスコア推移図に対応。

### p.8〜9 分析: iteration 数スケーリングと retained data 率・dimension ごとの挙動
- 内容: Figure 2/3 のイテレーションごとの平均スコアと retained data 割合、general/hallucination は単調増加だが一部次元でピーク後に悪化する非単調挙動、能力によって学習ダイナミクスが違うことの分析。
- 要約での扱い: `## イテレーションごとの伸び` で「合成データが効きやすい能力とそうでない能力が分かれている」として挙動の違いに言及。retained data 率の細かい数値は省略しているが、要点（どこが伸びるか／伸びないか）はカバー。

### p.8〜9（続き）分析: 多数決 vs 正解フィルタ（Figure 4）
- 内容: reasoning / VQA で多数決ベース vs 正解ベース vs データ量を揃えた多数決ベースの比較。多数決が 8.6% / 9.5% ほど優位で、データ量を揃えても差が残ること、理由として「多数決の方が一貫性ベースの信号になりやすい」ことを議論。
- 要約での扱い: `## 多数決とクローズドエンド` で、クローズドエンドタスクにおける多数決 vs 正解フィルタの比較と、データ量を揃えてもフィルタ方式自体の差が残ることを記述。`majority_vs_oracle.png` プレースホルダで Figure 4 に対応。

### p.10 分析・議論・制約
- 内容: self-improvement がマルチモーダル judge 構築に有望であること、safety など一部能力での限界、合成データの分布と実タスク分布のずれ、特に safety 評価に必要なインフラ（red-teaming など）が今回の枠組みの外にあることなどを整理。
- 要約での扱い: `# 議論はある？` で、人手／クローズド judge なしの利点、distribution mismatch による safety / reasoning の限界、一貫性フィルタの長所と限界をまとめて記述。

### p.11〜12 参考文献
- 内容: 関連する LLM-as-a-judge、VLM evaluator、synthetic data、hallucination 研究などの文献一覧。
- 要約での扱い: 直接の再述はしていないが、`# 先行研究と比べてどこがすごい？` と `# 次に読むべき論文は？` で代表的な流れ（Self-Rewarding LM, GPT-4V evaluator, RewardBench 系）をピックアップしている。

### p.13〜17 付録: イテレーション別 reasoning 例、judge プロンプト、detail alteration 用プロンプト集
- 内容: 同じペアに対する iteration ごとの reasoning 進化例、A/B 判定プロンプト、detail alteration を行うためのスタイルミミック系プロンプト群、データ生成時のプロンプトバリエーションなど。
- 要約での扱い: 具体的なプロンプト例や個別ケースはレポートの粒度外とし、省略。代わりに `## 擬似ペア生成` と `## 判定のふるい分け` で「どのような誤りを入れるか」「どのように A/B 判定させるか」を概念レベルでまとめている。

### p.18 ハイパーパラメータとコスト
- 内容: 温度 0.6, top_k=50, top_p=0.9、closed-ended で N=16 サンプル＋多数決閾値 5、学習率 1e-5, 5 epoch, H100 で約 400 GPU 時間、human annotation / GPT-4 distillation と比べたコスト感。
- 要約での扱い: データ生成サンプリング回数（16）や多数決を使う設計は `## 擬似ペア生成` のクローズドエンド説明に含まれるが、具体的な温度や GPU 時間などは省略。コストのオーダー感についても、本文では「安価に回せる」とだけ触れるにとどめている。

### p.19 付録: Correctness filter の負例
- 内容: 最終判定は正解だが reasoning が誤っている例（スタイル重視で誤りを見逃す）を挙げ、correctness ベースフィルタだけでは不十分であること、多数決／一貫性ベースフィルタの動機づけを補足。
- 要約での扱い: `## 多数決とクローズドエンド` と `# 議論はある？` で、「多数決や一貫性フィルタは強いが、誤った理由付けも残りうる」「理由の質までは保証されない」という形で反映。

## カバレッジ上のメモ
- 現状の要約は、イントロ・関連研究・手法（3ステージ）・主要実験・分析・議論の主張を一通りカバーしており、論文のコアメッセージとの大きな齟齬は見当たらない。
- 付録の具体的なプロンプトや個別ケース、細かいハイパーパラメータ、GPU コストなどは意図的に省略している。
- safety ベンチマークの詳細や red-teaming の具体策などは原文に譲っており、レポートでは「safety は伸びにくい」「専用インフラが必要」というレベルまでにとどめている。
