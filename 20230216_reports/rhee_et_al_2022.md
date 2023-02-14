# Countering Popularity Bias by Regularizing Score Differences

published date: 13 September 2022,
authors: Wondo Rhee, Sung Min Cho, Bongwon Suh
url(paper): https://dl.acm.org/doi/fullHtml/10.1145/3523227.3546757
url(presantation slide): https://dl.acm.org/action/downloadSupplement?doi=10.1145%2F3523227.3546757&file=Countering+Popularity+Bias+by+Regularizing+Score+Differences.pdf
(勉強会発表者: morinota)

---

## どんなもの?

- 多くの推薦システムでは、人気のアイテム(="short-head"なアイテム)は頻繁に推薦され、人気のないニッチなアイテム("long-tail"なアイテム)はほとんどor全く推薦されないという、Popularity Bias(人気度バイアス)に悩まされている.
- popularity biasは二種類に分けられる.
  - data bias: 多くの場合、学習データはアイテムの人気度においてロングテール分布を示している
  - model bias: 推薦システムは、ユーザが同じように好きなアイテムであっても、人気のあるアイテムに不当に高い推薦スコアを与えることがあり、その結果、人気のあるアイテムを過剰に推薦してしまう.
  - さらに，このような偏った推薦が feedback loop(?) を形成し，filter bubble やecho chamber(?)を引き起こす可能性がある.
    - feedback loop: 推薦結果をユーザに提供した際のfeedbackを受け取り、その結果を次の推薦に反映する事.
    - filter bubble: 推薦システムにより**ユーザが得られる情報が集約**されていく事. (それがユーザの嗜好と合致するバブルかは問わない)
    - echo chamber: 閉鎖的空間内でのコミュニケーションが繰り返されることにより、**特定の信念が増幅または強化されてしまう**状況の比喩.
- そこで本研究では，**推薦システムが各ユーザーのポジティブアイテム間で等しい推薦スコアを予測する(=人気アイテムのスコアを過剰に高くしない)**ように、損失関数にregularization termを追加することで，精度を維持したまま推薦結果の偏りを低減する新しい手法を提案する．

![Figure 1: The long-tail of item popularity. ](https://d3i71xaburhd42.cloudfront.net/6d77d7467f993780d02f3d8ea563959643d48f89/1-Figure1-1.png)

## 先行研究と比べて何がすごい？

- 既存手法は、精度向上と人気バイアス低減のトレードオフに悩まされる事が多い.

- 既存のdebias化を目的としたregularization term手法は、"itemの人気度とポジティブitemのスコアとの間のピアソン相関の大きさにペナルティを課す"ようなアプローチ. (なるほど...既存研究とはregularization termのpenalize対象が異なるのか...!!)
  - しかし、相関係数を正則化しても独立(=itemの人気度と独立になるって意味??)になるとは限らないこと，**計算コストがかかる**こと，という2つの制約がある.
- positive item内とnegative item内のスコア差をそれぞれ最小化するregularization termを用いて，精度を維持しつつmodel-biasを低減する方法を導入したのは，本研究が初めて.

## 技術や手法の肝は？

- $Pos_{u}$: ユーザ$u$がconsumeしたアイテムの集合
- $Neg_{u}$: ユーザ$u$がconsumeしなかったアイテムの集合.
- $\hat{y_{ui}}$: ユーザuがアイテムiに対して持つ予測嗜好に基づく推薦スコア(=推定されるパラメータ?)

既存のBRPの目的関数:

$$
Loss_{BPR} = - \sum_{u \in U} \sum_{p \in Po_{s_u}, n \in Ne_{g_u}} \log \sigma(\hat{y}_{u,p} - \hat{y}_{u,n})
\tag{1}
$$

- model-biasを測定するための指標: PopularityRank correlation for items (PRI, アイテムの人気度順位相関)
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

```python
def generate_sysnthetic_data(
    n_user: int = 200,
    n_item: int = 200,
) -> np.ndarray:
    user_item_matrix = np.zeros(shape=(n_user, n_item))
    for user_idx in range(n_user):
        for item_idx in range(n_item):
            user_item_matrix[user_idx, item_idx] = _get_synthetic_rating(
                user_idx,
                item_idx,
            )
    return user_item_matrix


def _get_synthetic_rating(user_idx: int, item_idx: int, boundary_num: int = 200) -> int:
    if user_idx + item_idx <= boundary_num:
        return 1
    return 0
```

このようなデータを用いて、ベースラインとして協調フィルタリング推薦システムの基本であるmatrix factorization (MF) modelを学習する. **損失関数としてBPR損失**を用いる.

また、提案手法も疑似データに対して学習させてみて、debias性能を検証した.
BPR損失に正則化項を追加した上で、同様のMFモデルを学習させ、ベースライン学習(=BPR損失)で見られたmodel-biasが緩和されるかどうかを確認する.

#### 結果:

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

hogehoge

以上のことから、**ZerosumはPos2Neg2法の簡易版である以上に、精度を向上させる効果がある**ことがわかった.

#### 他のdebias手法との比較.

提案手法の性能を，以下の先行研究debias手法と比較する.

- 逆傾向重み付け(IPW, inverse propensity weighting): model-biasを減らすために学習データに重みを適用する. ここで重みはitemの人気度の逆数. (i.e. 人気度の低いアイテムの学習優先度を上げるような方法...!)
- PD (Popularity-bias Deconfounding) 法: Causal interventionの一種.アイテムの人気度が推薦スコアに与える因果関係をモデル化し，その効果を除去する方法(因果推論的なアプローチだろうか...?? 例えば、アイテムの人気度が交絡因子みたいなイメージ??)
- Pearson regularization method: アイテム人気度と推薦スコアのPearson相関を0に近づけるような正則化項を損失関数に含める手法.

### 4つのベンチマークデータセットと4つの推薦モデルを用いた実証実験.

すべての先行手法はZerosum手法に比べ、精度が低いことがわかった.
IPWはdebias効果を示さず，PDは-0.52のPRI値を報告しており，これはモデルが不人気なitemを好んでいることを示している．
PDとPearsonは共に`PopQ@1`の値を0.3程度と報告し、Zerosum法よりも0.5(理想的な値)から遠い.

#### 結果:

## 議論はある？

## 次に読むべき論文は？

- 情報検索における検索結果多様化の先行研究[Exploiting Query Reformulations for Web Search Result Diversification](https://dl.acm.org/doi/pdf/10.1145/1772690.1772780?casa_token=_NkfT8SH_V4AAAAA:mkjn91maD3dGMMF6GbfFSbmOqqa9tfqBDohAO26vAytPbVt0BQidOPWX0tL4EsUkRD00tJ-4CrMWAQ)
- regularized long-tail diversification algorithmに関する論文 [Controlling Popularity Bias in Learning to Rank Recommendation](https://dl.acm.org/doi/10.1145/3109859.310991

## 実装するとしたら、なんとなくこんな感じ...?
