# ソース網羅性チェック

> 注: 今回は `read-arxiv-paper` で展開済みだった TeX ソース
> (`/tmp/read-arxiv-paper/2602.15030/icml2026.tex`) と同梱図表 PDF を一次資料として確認しました。
> ローカルに公式 PDF を再取得できなかったため、このファイルでは PDF ページ単位ではなく、
> 節・図表単位で要約と画像の根拠を整理しています。

| 対応箇所 | 主な記載 | 要約・画像での反映 |
| --- | --- | --- |
| Abstract, Sec. 1 | 提案の全体像、1-step / few-step 生成、VAE の posterior hole 問題 | 「# どんなもの？」「# 先行研究と比べてどこがすごい？」 |
| Fig. 2, Sec. 2.1, Eq. (1)-(3) | 球面潜在空間と直接サンプリング | 「## 球面潜在空間」、`sphere_latent_overview.png` |
| Fig. 4, Sec. 2.2, Eq. (4)-(5) | noisy spherify と `σ` jitter | 「## ノイズ付き spherify」、`noisy_spherification_pipeline.png` |
| Sec. 2.3, Eq. (7)-(10) | 3 つの損失とその役割 | 「## 損失設計」 |
| Sec. 2.4, Algorithm 1 | ViT + MLP-Mixer、conditional encoder、few-step inference | 「## アーキテクチャと few-step 生成」 |
| Table 1, Sec. 3.1, Fig. 5 | CIFAR-10 の conditional / unconditional 結果 | 「# どうやって有効だと検証した？」、`cifar_few_step_results.png` |
| Table 2, Table 3, Sec. 3.2-3.3 | Oxford-Flowers / Animal-Faces / ImageNet の比較、FID と知覚品質のズレ | 「# どうやって有効だと検証した？」「# 議論はある？」 |
| Sec. 4, Fig. 7 | conditional uniformity と latent 可視化 | 「## アーキテクチャと few-step 生成」 |
| Sec. 5, Fig. 8-9 | training-free editing と image crossover | 「## アーキテクチャと few-step 生成」、`conditional_editing_examples.png` |
| Sec. 6, Fig. 10-13, Table 4-6 | noise angle、loss ablation、sampling scheme | 「# どうやって有効だと検証した？」、`noise_angle_ablation.png` |
| Appendix A-C | CFG 位置、memorization、追加 ablation | 「# 議論はある？」 |
| Sec. 8 | proof-of-concept、学習コスト、将来展望 | 「# 議論はある？」 |

# 根拠チェック

## どんなもの？
- Abstract
  - "capable of producing images in a single forward pass"
  - "competing with many-step diffusion models using fewer than five steps"
- Sec. 1
  - "maps the distribution of natural images uniformly onto the sphere"
  - "an image is generated quickly by sampling a random point on the sphere"

## 先行研究と比べてどこがすごい？
- Sec. 1
  - latent diffusion は VAE の latent を diffusion が補うという整理です。
  - Sphere Encoder は「a spherical latent space ... can be learned so precisely that the expensive diffusion step is irrelevant」と述べています。
- Sec. 7
  - few-step diffusion や consistency model は既存軌道の近似であり、本手法はそこから外れた direct sampling 系として位置づけています。

## 技術や手法の肝は？
- Eq. (1)-(3)
  - `v = f(E(x))`
  - `x_hat = D(v)`
  - `x_hat = D(f(e))`
- Eq. (4)-(5)
  - `v_NOISY = f(v + σe)` と `σ = r * σ_max`
- Eq. (7)-(10)
  - pixel reconstruction、pixel consistency、latent consistency の 3 損失
- Algorithm 1
  - 1-step 生成と few-step encode-decode refinement の擬似コード

## どうやって有効だと検証した？
- Table 1
  - CIFAR-10 conditional: gFID 18.68 -> 2.72 -> 1.65
  - CIFAR-10 unconditional: gFID 35.67 -> 4.31 -> 2.34
- Table 2
  - Oxford-Flowers with CFG: 1-step 25.12, 4-step 11.25
  - Animal-Faces: 1-step 21.70, 6-step 17.97
- Table 3
  - ImageNet Sphere-L: gFID 4.76 / IS 301.8
  - ImageNet Sphere-XL: gFID 4.02 / IS 265.9
- Table 4-6
  - 3 損失の加算で gFID が改善
  - fixed noise strength + shared noise が最良

## 議論はある？
- Sec. 3.3
  - "low FID scores do not always align with perceptual realism"
  - sampling steps を増やすと FID は下がるが、global semantic coherence を損なうことがあると議論しています。
- Sec. 8
  - "proof-of-concept"
  - encoder と decoder の両方にパラメータが必要で、学習時に encoder を 2 回通すのが欠点だと述べています。
- Appendix B
  - CIFAR-10 を長く学習すると near-duplicate が出る例を示しています。

## 画像ごとの根拠
- `sphere_latent_overview.png`
  - `figs/intro.pdf` 由来です。
  - Figure 2 の「自然画像分布を球面へ写し、球面上のランダム点を decode する」という全体像を示します。
- `noisy_spherification_pipeline.png`
  - `figs/model.pdf` 由来です。
  - Figure 4 の noisy spherify と再投影を示します。
- `cifar_few_step_results.png`
  - `figs/cifar.pdf` 由来です。
  - Figure 5 の step 数ごとの CIFAR-10 生成品質の違いを示します。
- `conditional_editing_examples.png`
  - `figs/cond_manipulation.pdf` 由来です。
  - Figure 8 の class-conditioned editing 例を示します。
- `noise_angle_ablation.png`
  - `figs/sigma_angle_curv.pdf` 由来です。
  - Figure 10 の noise angle `α` に対する性能変化を示します。
