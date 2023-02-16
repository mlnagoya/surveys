# Countering Popularity Bias by Regularizing Score Differences

published date: 13 September 2022,
authors: Wondo Rhee, Sung Min Cho, Bongwon Suh
url(paper): https://dl.acm.org/doi/fullHtml/10.1145/3523227.3546757
url(presantation slide): https://dl.acm.org/action/downloadSupplement?doi=10.1145%2F3523227.3546757&file=Countering+Popularity+Bias+by+Regularizing+Score+Differences.pdf
(勉強会発表者: morinota)

---

## どんなもの?

- 多くの推薦システムでは、人気のアイテム(="short-head"なアイテム)は頻繁に推薦され、人気のないニッチなアイテム("long-tail"なアイテム)はほとんどor全く推薦されないという、Popularity Bias(人気度バイアス)に悩まされている.
- 本論文では，Popularity Bias、特に，ユーザが同じように好きなアイテムの中で人気のあるアイテムに高いスコアを与えてしまう**model-bias**に着目し，解決を試みている.
- 本論文は，**推薦システムが各ユーザのポジティブアイテム間で等しい推薦スコアを予測する(=人気アイテムのスコアを過剰に高くしない)**ように、BPR損失関数にregularization termを追加することで，精度を維持したまま推薦結果のbiasを低減する新しい手法を提案する．

Popularity biasとはこういう話でした...!(先月の論文読み会で読んだ論文より)
![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1697279/6b6f12c4-dd34-d41c-ee07-32cb965da284.png)

## 先行研究と比べて何がすごい？

- 既存手法は、精度向上とmodel-bias低減のトレードオフに悩まされる事が多い.
- 既存のdebias化を目的としたregularization term手法は、"itemの人気度とポジティブitemのスコアとの間のピアソン相関の大きさにペナルティを課す"ようなアプローチ. (=推薦スコアと人気度の間の相関を低くするようなアプローチ...!)
  - しかし、相関係数を正則化しても独立(=itemの人気度と推薦結果が独立になるって意味??)になるとは限らないこと，**計算コストがかかる**こと，という2つの制約がある.
- **positive item内とnegative item内のスコア差をそれぞれ最小化**するregularization termを用いて，精度を維持しつつmodel-biasを低減する方法を導入したのは，本研究が初めて.
- 疑似データを用いた実験 & ベンチマークデータを用いた実験 にて、先行研究のdebias手法と比較して, 最小限の精度低下 & 高いdebias性能を観測.

## 技術や手法の肝は？

問題設定:

- $Pos_{u}$: ユーザ$u$がconsumeしたアイテムの集合
- $Neg_{u}$: ユーザ$u$がconsumeしなかったアイテムの集合.
- $\hat{y_{ui}}$: ユーザuがアイテムiに対して持つ予測嗜好に基づく推薦スコア(=推定されるパラメータ?)

既存のBRP(の目的関数:

$$
Loss_{BPR} = - \sum_{u \in U} \sum_{p \in Po_{s_u}, n \in Ne_{g_u}} \log \sigma(\hat{y}_{u,p} - \hat{y}_{u,n})
\tag{1}
$$

model-biasを測定するために２つの評価指標を採用.
一つ目は、 PopularityRank correlation for items (PRI, アイテムの人気度順位相関)

- アイテムの人気度と平均ランキング位置の**Spearman rank correlation coefficient(SRC, スピアマン順位相関係数)**
- SRC(スピアマンの順位相関係数):
  - 順位データから求められる相関の指標.(初めて聞いた...!)
  - $\rho = 1 - \frac{6 \sum D^2}{N^3 - N}$ で定義される.
  - ここで、$N$は値のペアの数. $D$は対応する変数Xと変数Yの値の**順位の差**
  - XとYの２つの順位の傾向が等しい=正の(線形)相関が強い場合は$\rho=1$に近づく.
  - [wikipediaより](https://ja.wikipedia.org/wiki/%E3%82%B9%E3%83%94%E3%82%A2%E3%83%9E%E3%83%B3%E3%81%AE%E9%A0%86%E4%BD%8D%E7%9B%B8%E9%96%A2%E4%BF%82%E6%95%B0)

$$
PRI = SRC (popularity(I), ave_rank(I))
\tag{2}
$$

ここで、

- 各アイテムiの `ave_rank`: 各アイテムiについて、$Pos_{u}$にiを持つ各ユーザーuを探し出し、$Pos_{u}$内でのiのランク位置の分位数(=0 ~ 1?)を計算する. 次に、$Pos_{u}$内でiを持つ全てのユーザuの順位位置の分位数を平均する.
- PRIは、"アイテムの人気度"と"推薦モデルのスコアに基づく平均ランキング位置"のSRCなので...
- PRI値が1に近い程、人気のあるアイテムに高いスコアを与えるモデル->model-biasが大きいと言える.
- 0 に近いほど，ポジティブなアイテムの人気と推薦スコアランキングに相関がない. -> model-biasが小さいことを意味する．

また、各ユーザーのpositiveアイテムのスコア一位の平均人気度分位値（PopQ@1）を計算する指標を式(3)提案する.

$$
PopQ@1 = \frac{1}{|U|}\sum_{u\in U} \text{PopQuantile}_u(\argmax_{x\in Po_{s_u}}(\hat{y}_{ui}))
\tag{3}
$$

ここで,

- $\text{PopQuantile}_u$ : $Pos_{u}$内の、あるアイテムの人気度分位.
  - $Pos_{u}$内でグローバルな人気が最も高いアイテム-> $\text{PopQuantile}_u=0$
  - グローバルな人気が最も低いアイテム->$\text{PopQuantile}_u=1$
  - 各ユーザのpositiveアイテムのスコア一位は、通常(=model-biasを解決してないケース!)グローバルな人気が高いpositive itemになるので、` PopQ@1` が 0 に近い場合(=sumの合計値が小さい!)はmodel-biasが大きいことを意味する.
  - 一方、PopQ@1 の値が 0.5 に近い場合は、人気度分位が 0 と 1 の間に分散している可能性が高いため、model-biasがないことを意味する.

この2つの指標により、model-biasを詳細に評価することができる.

推薦システムにとって重要なことは、model-biasを抑えながら精度を維持すること.
model-biasが少なくても精度が低ければ、個人に合った推薦を行うことはできない.
例えば、ランダムな推薦を行うモデルは、model-biasを示さないが、ユーザの嗜好を全く考慮しない.

### Proposed Method

model-biasを減らすために、我々は**BPR損失関数にregularization termを追加**して拡張し、positive & negativeアイテム間のスコア差をそれぞれ最小化する方法を提案する. (**positive同士、negative同士のスコアを近くしたい...!!**)

BPR損失はpositive item と negative item の推薦スコアを対比させるが、追加するregularization termはさらに、positive (negative) item内でスコアが等しくなるように強制する.

提案する損失関数は以下.

$$
\text{Total Loss} = \text{BPR Loss} + \text{Reg Term}
\tag{5}
$$

論文では、**regularization term のバリエーションを2つ**提案している.

- **Pos2Neg2 Term**: 1ユーザにつき2つのpositive item(`p_1`, `p_2`)と2つのnegative item(`n_1`, `n_2`)を同時にサンプリングし、それぞれpositive item(negative item)のスコア差を最小にする.

$$
\text{Reg Term} = - \sum_{u \in U} \sum_{p_1, p_2 \in Pos_{u}, n_1, n_2 \in Neg_{u}}
\log (1 - \tanh(|\hat{y}_{u, p_1} - \hat{y}_{u, p_2}|))
+ \log (1 - \tanh(|\hat{y}_{u, n_1} - \hat{y}_{u, n_2}|))
\\
\tag{6}
$$

- **Zerosum Term**: : 一人のユーザに対してpositive item と negative item をそれぞれ1つずつサンプリングし、positive item と negative item の推薦スコアの和が0に近づくように正則化する.
  - 学習により、正則化はユーザのランダムなpositive-negative itemペアに伝播し、positive itemと negative item が対称的な推薦スコアを持つことを余儀なくされる.
  - 最終的には、positive itemのスコアは単一の値に収束し、negative itemのスコアは対称的な値に収束する.

$$
\text{Reg Term} = - \sum_{u \in U} \sum_{p \in Pos_{u}, n \in Neg_{u}}
\log (1 - \tanh(|\hat{y}_{u, p} + \hat{y}_{u, n}|))
\\
\tag{7}
$$

どちらのReg Termも、positive(negative)のアイテムに対して等しいスコアを与えるようにモデルを導くことで、model-biasを減らすことを目的としている.

本アプローチには2つの利点がある．

- 第一に，精度とdebiasのトレードオフに対してrobust.
  - 全itemのスコアを一括して調整するdebias手法と比較して，提案手法はpositive itemのスコアを犠牲にしてnegative itemのスコアを上げることがない．
- 第二に，単純であること.
  - 提案手法はBPR損失を用いるどのようなモデルにも適用可能.

実験ではpositive item のスコアだけを正則化すると精度が悪化することがわかったので、positiveとnegativeの両方に正則化を適用している.

## どうやって有効だと検証した?

### ベースライン学習にmodel-biasを誘発するような、疑似データセットを用いた実験.

本研究では、model-biasとそれに続く様々な手法のdebias性能を説明するために、data-biasを明示した合成データを設計する.

- 200 x 200のuser-item interaction matrix $R$
- 式(4)を使って疑似データを生成: アイテム列のindexが増加するにつれてアイテムの人気が直線的に減少するように設定.
- 行列は binary(0 or 1) のinteraction情報で満たされている.
- このようなデータは、疎でノイズの多い実世界のデータからは逸脱しているが、**推薦システムがどのようにmodel-biasを生み出すか**を観察するには適切.

疑似データ生成方法をコードにするとこんな感じ.

```python: sample.pys
def generate_sysnthetic_data(
    n_user: int = 200,
    n_item: int = 200,
) -> sparse.csr_matrix:
    user_item_matrix_array = np.zeros(shape=(n_user, n_item))
    for user_idx in range(n_user):
        for item_idx in range(n_item):
            user_item_matrix_array[user_idx, item_idx] = _get_synthetic_rating(
                user_idx,
                item_idx,
            )
    return sparse.csr_matrix(user_item_matrix_array)


def _get_synthetic_rating(user_idx: int, item_idx: int, boundary_num: int = 200) -> int:
    if user_idx + item_idx <= boundary_num:
        return 1
    return 0
```

このようなデータを用いて、ベースラインとして協調フィルタリング推薦システムの基本であるmatrix factorization (MF) modelを学習する. **損失関数としてBPR損失**を用いる.

また、提案手法も疑似データに対して学習させてみて、debias性能を検証した.
BPR損失に正則化項を追加した上で、同様のMFモデルを学習させ、ベースライン学習(=BPR損失)で見られたmodel-biasが緩和されるかどうかを確認する.

#### 結果:

![](https://dl.acm.org/cms/attachment/af5498b4-9f16-40e8-a374-488c975453ca/recsys22-6-fig1.jpg)

- 図1aは疑似データを行列形式で表したもので、白い部分がpositive item(1)、黒い部分がnegative item(0)に相当する.
- 図1bは学習したMFモデル(ベースライン)の推薦スコアであり、model-biasが顕著に表れている.
  - positiveアイテムにおいて、人気のあるアイテム(=item indexが小さい)ほど高いスコアを推論している.
  - ex) `user_idx=100`の場合、ユーザは `item_idx=0 ~ 100`のアイテムを同じようにconsume(=click等, 何らかのreaction)しているにもかかわらず、モデルは`item_idx=0 ~ 20`の人気アイテムに高いスコアを予測している.

以下、モデルのaccuracyとdebias性能の定量的評価:

- BPR損失関数を用いて学習したモデルは高い精度を示していた.
- `PRI`と`PopQ@1`によるdebias性能:
  - 図1cは、x軸が疑似データの`item_idx`を示し、アイテムの平均ランク分位を示したもの（i.e. x軸の値が小さいアイテムほど人気がある).
    - 平均的に最も人気のあるアイテムは、positiveアイテムの中で上位0.0%にランクされる. アイテムの人気が低下すると、そのアイテムはもはや最高ランクではなくなる.
    - **これはmodel-biasが大きいことを示しており、PRIも0.99と計算される.**
  - 図1dは、各ユーザのpositive itemのtopスコアの人気度分位をヒストグラムにしたもの.
    - 人気度分位は0付近に集中しており、topスコアのpositive itemはほとんど最も人気のあるpositive itemで構成されていることが分かる.
  - `PRI`と`PopQ@1`の両メトリクスは、BPR損失で学習したモデルが高いmodel-biasの存在を示している.

提案手法を疑似データに適用した結果:

![fig_2](https://pbs.twimg.com/media/FdJXTGEaEAEWsAy?format=jpg&name=4096x4096)

- 図2は、ベースラインモデル(BPR損失関数によるMF)と提案手法(BPR損失+正則化項のMF)を用いた場合の、モデル出力値(推薦スコア).
  - 精度に関する評価(fig2-a~c):
  - debias 性能に関する評価(fig2-d~f):
    - 上のグラフ: positive itemの平均順位分位数.
      - 提案手法では、人気アイテム（小アイテムインデックス）を含むほとんどのアイテムで平均順位が0.25～0.75程度となり、**順位が人気の影響を受けなくなったことがわかる**.
      - しかし、人気度の低いtail item（アイテムインデックス190〜200）は依然として平均順位が最下位であり、tail itemに対してdebiasは有効でなかったことがわかる.
    - 下のグラフ: 各ユーザのpositive itemのスコアtopの人気度分位値のヒストグラム.
      - Pos2Neg2法、Zerosum法ともに、人気度分位は0〜1に広がっている.
      - 表1より、PopQ@1`はそれぞれ0.62、0.61と計算され、理想の0.5により近づいていることがわかる.

これらの結果から、提案した正則化項はいずれも高い精度を維持しつつ、model-biasを低減する効果があることがわかる.

#### 2つの提案手法の比較.

- Zerosum法はPos2Neg2法よりも高い精度を出した.
-

以上のことから、**ZerosumはPos2Neg2法の簡易版である以上に、精度を向上させる効果がある**ことがわかった.

#### 他のdebias手法との比較.

提案手法の性能を，以下の先行研究debias手法と比較した.

- 逆傾向重み付け(IPW, inverse propensity weighting): model-biasを減らすために学習データに重みを適用する. ここで重みはitemの人気度の逆数. (i.e. 人気度の低いアイテムの学習優先度を上げるような方法...!)
- PD (Popularity-bias Deconfounding) 法: Causal interventionの一種.アイテムの人気度が推薦スコアに与える因果関係をモデル化し，その効果を除去する方法(因果推論的なアプローチだろうか...?? 例えば、アイテムの人気度が交絡因子みたいなイメージ??)
- Pearson regularization method: アイテム人気度と推薦スコアのPearson相関を0に近づけるような正則化項を損失関数に含める手法.

![](https://dl.acm.org/cms/attachment/4724d5c2-b5ca-4e9e-b354-b8d1d5736e68/recsys22-6-fig3.jpg)

- 逆傾向重み付け(IPW, inverse propensity weighting)
  - 図3aより、IPW法はpositive itemとnegative item の対比的な preference を明確に区別することができないことがわかる.
  - また、図3dの結果からわかるように、この手法はmodel-biasを減らすことができなかった.
- PD (Popularity-bias Deconfounding) 法:
  - 図3bは、PD法が満足のいくデビアス性能を発揮し、かつ、ポジティブとネガティブの preference を正確に区別していることを示している.
  - しかし、debiasは全てのアイテムで均一ではない. 図3eの上側のグラフでは、平均的なitemのランク分位が曲線的な形状を示し、**最も人気のある項目が依然として上位にランクされていることがわかる**.
- Pearson regularization method:
  - 図3cは、Pearson法では、**あるユーザ（例：ユーザインデックス0〜20）では人気アイテムのスコアが低く、他のユーザ（例：ユーザインデックス100〜200）では高くなる**ことを示している.
    - ex) user_index 0〜20のユーザには、人気アイテムの推薦スコアが過剰に低くなる.
    - いわば、**異なる方向のmodel-biasを追加**(人気なアイテムをあえてオススメしないようにする?)している状況...??
  - 図3fの上のグラフは、人気アイテム（アイテムインデックス0〜20）のaverage rank quantile が0.5に近いことを示しているが、残りのアイテムについてはmodel-biasが減少していないことがわかる.
  - 図3fの下側のグラフは、popularity quantiles が公平に広がっていることを示している.

### 4つのベンチマークデータセットと4つの推薦モデルを用いた実証実験.

すべての先行手法はZerosum手法に比べ、精度が低いことがわかった.
IPWはdebias効果を示さず，PDは-0.52のPRI値を報告しており，これはモデルが不人気なitemを好んでいることを示している．
PDとPearsonは共に`PopQ@1`の値を0.3程度と報告し、Zerosum法よりも0.5(理想的な値)から遠い.

## 議論はある？

Pearson regularization methodと提案debias手法の比較:

Pearson regularization methodでは、本来のBPR損失関数に，「positive itemに対してitem人気度と推薦スコアの相関の大きさを制限する正則化項」を加える手法を提案している.
この方法は，negative itemの推薦スコアを押し上げることなく、positive itemのスコアのみをバランスさせることを目的としており、従ってこの方法は精度とバイアスのトレードオフに対してよりロバスト.
(この点に関しては、提案手法であるZerosum法も同様のモチベーションを持っている.)

Pearson regularization methodの欠点:

- 計算の妥当性
  - 図3cから、Pearson法は**人気itemのスコアを選択的に下げる事で相関係数を0に近づけており、意図したitemの人気とスコアの独立性が達成されていない**. (人気アイテムのスコアを選んで下げている = 逆のmodel-bias??)
  - これに対して、Zerosum法はより単純なロジックを採用しており、debiasedスコア(=model-biasを取り除いたスコア)を直接予測するのに有効.
- 計算効率:
  - Pearson regularization methodでは、1回の学習ですべてのpositive itemのスコアを計算する必要があり、計算コストがかかる.(ミニバッチ学習ができない)
  - これに対して、Zerosum法では、通常のBPR損失関数と同様に**学習データの一部をサンプリングして**損失関数を計算できるので, ミニバッチ学習が可能(メモリ効率 & 計算量の話?)

## 次に読むべき論文は？

- BPRの元論文は読んでおいた方が良さそう.[BPR: Bayesian Personalized Ranking from Implicit Feedback](https://arxiv.org/ftp/arxiv/papers/1205/1205.2618.pdf)
- 6 Feb 2023 にpublishされた 推薦システム入門編の論文 [Recommender Systems: A Primer](https://paperswithcode.com/paper/recommender-systems-a-primer)

## お気持ち実装

実装するとしたら、なんとなくこんな感じ...?

```python: model.py
from typing import List, Tuple

import torch
import torch.nn as nn
from scipy import sparse
from torch import Tensor
from torch.utils.data import DataLoader, Dataset


class BPRLossZerosumRegularized(nn.Module):
    """BPR損失関数 + Zerosum法による正則化項"""
    def __init__(
        self,
        is_regularized: bool = True,
        eps: float = 1e-8,
    ) -> None:  # 小さい値をepsとして定義
        super(BPRLossZerosumRegularized, self).__init__()
        self.is_regularized = is_regularized
        self.eps = eps

    def forward(self, positive_scores: Tensor, negative_scores: Tensor) -> Tensor:
        # self._print_scores(positive_scores, negative_scores)
        score_diffs = torch.sigmoid(positive_scores - negative_scores)

        score_diffs = torch.clamp(score_diffs, min=self.eps, max=1.0)  # score_diffsの値をクリップ
        loss = -torch.sum(torch.log(score_diffs))
        # Add regularization term to the loss
        if self.is_regularized:
            loss -= self._calc_zerosum_reg_term(positive_scores, negative_scores)
        return loss

    def _calc_zerosum_reg_term(
        self,
        positive_scores: Tensor,
        negative_scores: Tensor,
    ) -> Tensor:
        """Zerosum Term:
        - 各ユーザに対して、positive item と negative item
        をそれぞれ1つずつサンプリング.
        - positive item と negative item の推薦スコアの和が
        0に近づくように正則化する.
        - 最終的には、positive itemのスコアは単一の値に収束し、
        negative itemのスコアは対称的な値に収束する.
        - 引数にて、すでにユーザ毎にサンプリングされてきたscoresが渡される想定.
        """
        scores_sum = positive_scores + negative_scores
        return torch.sum(torch.log(1 - torch.tanh(scores_sum)))

    def _print_scores(self, pos_scores: Tensor, neg_scores: Tensor) -> None:
        for idx in range(pos_scores.shape[0]):
            print(pos_scores[idx], neg_scores[idx])


class MatrixFactorization(nn.Module):
    """提案された損失関数を適用するベースモデル"""
    def __init__(
        self,
        num_users: int,
        num_items: int,
        embedding_dim: int,
        is_regularized: bool = True,
    ) -> None:
        """
        user_num: number of users;
        item_num: number of items;
        factor_num: number of predictive factors.
        """
        super(MatrixFactorization, self).__init__()
        self.embed_user = nn.Embedding(num_users, embedding_dim)
        self.embed_item = nn.Embedding(num_items, embedding_dim)
        self.is_regularized = is_regularized

    def forward(self, user_indices: Tensor, item_indices: Tensor) -> Tensor:
        user_embeddings: Tensor = self.embed_user.forward(user_indices)
        item_embeddings: Tensor = self.embed_item.forward(item_indices)
        preference_scores = torch.sum(user_embeddings * item_embeddings, dim=1)
        return preference_scores

    def fit(
        self,
        user_item_reactions: sparse.csr_matrix,
        loss_func: BPRLossZerosumRegularized,
        optimizer: torch.optim.Optimizer,
        batch_size: int,
        num_epochs: int,
        device: torch.device,
    ) -> List[float]:
        """BPRの学習を実行する."""
        self.to(device)
        loss_history = []
        train_data = self._sampling_dataset(user_item_reactions)
        train_dataloader = DataLoader(train_data, batch_size, shuffle=True)
        for epoch_idx in range(num_epochs):
            self.train()
            running_loss = 0.0
            for batch in train_dataloader:
                user_indices, pos_item_indices, neg_item_indices = batch
                user_indices: Tensor = user_indices.to(device)
                pos_item_indices: Tensor = pos_item_indices.to(device)
                neg_item_indices: Tensor = neg_item_indices.to(device)

                optimizer.zero_grad()
                pos_scores = self.forward(user_indices, pos_item_indices)
                neg_scores = self.forward(user_indices, neg_item_indices)

                print(pos_scores)

                loss = loss_func.forward(pos_scores, neg_scores)
                print(loss)
                running_loss += loss.item()
                loss.backward()
                optimizer.step()

            print(f"Epoch {epoch_idx + 1}, loss={running_loss:.4f}")
            loss_history.append(running_loss)
        return loss_history

    def _sampling_dataset(self, user_item_reactions: sparse.csr_matrix) -> Dataset:
        """implicitデータである user_item_reactionsから、
        (u, i, j) \in D_sのTripletをサンプリングしてDatasetとして返す.
        """
        pass
```

テストコード

```python: test_model.py
import numpy as np
import pytest
import torch
from model import BPRLossZerosumRegularized, MatrixFactorization
from scipy import sparse
from torch.utils.data import DataLoader, TensorDataset


@pytest.fixture
def bpr_reg_loss_func() -> BPRLossZerosumRegularized:
    return BPRLossZerosumRegularized(is_regularized=True)


@pytest.fixture
def mf_model() -> MatrixFactorization:
    return MatrixFactorization(num_users=100, num_items=50, embedding_dim=16)


@pytest.fixture
def user_item_reactions() -> sparse.csr_matrix:
    user_ids = [1, 2, 3]
    item_ids = [1, 2, 3]

    reactions = np.array([1, 1, 1])
    user_indices = np.array([0, 1, 2])
    item_indices = np.array([1, 0, 2])

    return sparse.csr_matrix((reactions, (user_indices, item_indices)), shape=(len(user_ids), len(item_ids)))


def test_bpr_loss(bpr_reg_loss_func: BPRLossZerosumRegularized) -> None:

    # create some test data
    positive_scores = torch.tensor([3.0, 2.0, 4.0])
    negative_scores = torch.tensor([1.0, 1.5, 1.0])

    # calculate expected loss
    expected_loss = (
        # BPR Loss Term
        - torch.log(torch.sigmoid(positive_scores[0] - negative_scores[0]))
        - torch.log(torch.sigmoid(positive_scores[1] - negative_scores[1]))
        - torch.log(torch.sigmoid(positive_scores[2] - negative_scores[2]))
        # Zerosum Regularization Term
        + torch.log(1 - torch.tanh(positive_scores[0] + negative_scores[0]))
        + torch.log(1 - torch.tanh(positive_scores[1] + negative_scores[1]))
        + torch.log(1 - torch.tanh(positive_scores[2] + negative_scores[2]))
    )

    actual_loss = bpr_reg_loss_func.forward(positive_scores, negative_scores)

    assert torch.isclose(actual_loss, expected_loss)


def test_train_bpr(
    mf_model: MatrixFactorization,
    user_item_reactions: sparse.csr_matrix,
    bpr_reg_loss_func: BPRLossZerosumRegularized,
) -> None:
    optimizer = torch.optim.Adam(mf_model.parameters(), lr=0.01)
    num_epochs = 2
    loss_histroy = mf_model.fit(
        user_item_reactions,
        bpr_reg_loss_func,
        optimizer,
        batch_size=32,
        num_epochs=num_epochs,
        device=torch.device("cpu"),
    )

    assert len(loss_histroy) == num_epochs

    for epoch_loss in loss_histroy:
        assert epoch_loss >= 0
```
