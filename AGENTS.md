# Repository Guidelines

## プロジェクト構成
- `<basename>` = `<topic>_<arXivID>`（例: `idefics2_2405.02246`）。
- 各 Markdown と同名のアセット用フォルダを併設: 例) `UnSAM_2406.20081.md` と `UnSAM_2406.20081/`。
- 画像は相対パスで参照: `![説明](./<md_basename>/image.png)`。
  例: `20240516_reports/idefics2_2405.02246/fromage.png`。
  - レポート本文には意味のある内容を示す画像を複数枚挿入し、ファイル名も内容が推測できるものにする（例: `figure1_pipeline.png`）。`placeholder` 等の汎用名やダミー画像は禁止。
  - 画像は原則として対象論文 PDF からの切り抜きを使用し、必要に応じて PyMuPDF 等で適切な領域をトリミングする。
  - 画像と同じディレクトリに `coverage_evidence.md` を作成し、PDF各ページの網羅性と要約・画像の根拠（ページ番号と引用）を整理する。
 - 最終配置のパス規約（重要・要確認）:
   - 最終版の Markdown は日付フォルダ直下に置く（例: `20250918_reports/auras_2509.09560.md`）。
   - 同名のアセットフォルダを同じ日付フォルダ直下に併設（例: `20250918_reports/auras_2509.09560/`）。
   - 追加のサブディレクトリ（`/auras/auras_2509.09560.md` のような二重ネスト）は作らない。
   - 画像参照は `./<md_basename>/...`（例: `./auras_2509.09560/fig1.png`）。

## ビルド・プレビュー・開発
- ビルドは不要。任意のエディタ/ビューアで Markdown を開いて確認。
- 便利なコマンド例:
  - レポート一覧: `find . -maxdepth 2 -type d -name '*_reports'`
  - 文字列検索: `rg -n "keyword" 2025* 2024* 2023*`
  - ツリー表示: `tree -L 2 2024*`（`tree` がある場合）



## スタイルと命名規約（n-kats 準拠）
- 先頭3行の書式:
  1) H1 に論文タイトル  2) arXiv URL  3) `(まとめ @github_id)`。
- 著者情報: 先頭3行の直後に「著者」セクションを置き、arXiv もしくは PDF の記載に従って著者名を箇条書きで列挙（所属は任意、外部リンクは最小限）。
  - 著者表記ルール: 人名はアルファベット表記のみ可（原文の arXiv/PDF 準拠）。カタカナ・漢字・和訳は不可。1ファイル内で表記を統一すること。
- 見出しの順序（例）:
  `# どんなもの？` → `# 先行研究と比べてどこがすごい？` → `# 技術や手法の肝は？` →
  `# どうやって有効だと検証した？` → `# 議論はある？` → `## 私見` → `# 次に読むべき論文は？`。
  - 主要セクションは基本的に `#` 見出しで統一し、補助的な節を追加する場合は `##` 以降の階層を適宜利用（例として「## 私見」）。
- 命名:
  - Markdown: `<topic>_<arXivID>.md`（例: `idefics2_2405.02246.md`）。
  - 画像フォルダ: `<topic>_<arXivID>/` に配置（例: `./idefics2_2405.02246/arch.png`）。
  - 画像名: `snake_case.ext`、サイズは概ね < 2 MB。
- 箇条書きを優先、1行は約100文字目安。
- タイトル直後に「著者」セクションを置き、本文は原則として `#` 見出しをベースにしつつ、必要に応じて `##` などの下位見出しを追加する。
- 既存ファイルの更新では `cat > file` 等の破壊的上書きは避け、`apply_patch` など差分ベースの編集手段を使う。
 - 表記統一（一般）:
   - 用語・語彙は文書内で表記を統一（英語/日本語の混在を避ける）。
   - 英語の技術語は原綴りで統一するか、日本語訳で統一するかを選ぶ（併記はしない）。
   - 日本語表記の注意: 日本語で統一する場合は不自然な直訳・誤用・不慣用な訳語を避け、専門分野で自然な表現を用いる。適切な日本語がない場合は英語原綴りを採用。
   - 数値・単位・半角/全角・句読点（、。）の使い方を統一。
   - 略語は初出で展開し、以降は略語に統一（例: Key-Value → KV）。

## テスト/品質確認
- 各レポートで手動確認:
  - 画像が表示される（相対パスのみ）。
  - 参照リンクが解決する。外部直リンクは極力避ける。
  - 大文字小文字の不一致がない。
  - 著者セクションがあり、表記揺れや欠落がない。
- 任意ツール: `markdownlint '**/*.md'`、リンクチェッカー等。
- 例外: エージェントの草案（`_tmp/`配下）はプレースホルダ画像の記述を許容（後続PRで実画像に差替/削除）。
 - プレースホルダを最終要約に残す場合: alt/キャプションに「想定」を明記し、リンク切れは許容（後続PRで実画像を追加）。

## コミット/PR ガイドライン
- コミットは現在形＋スコープ接頭辞:
  - `report: add 20241017 patchcore summary`
  - `assets: compress blip2 figures`
  - `docs: fix links in 20240321 README`
- PR には以下を含める:
  - 変更概要と影響パス、必要に応じてプレビュー画像。
  - 課題リンク（あれば）とチェックリスト（画像/リンク/ファイル名確認）。
  - n-kats 準拠かの確認（先頭3行・見出し順・相対パス）。

## セキュリティ/アセット
- 画像の EXIF 等のメタデータは必要に応じて除去。
- 図や本文、ファイル名に機微情報を含めない。
- 図は可逆圧縮を優先。軽量であればソース（例: `*.drawio`）も保存。

## エージェント向け指示（役割と手順）
- 既定言語: 基本的な応答は日本語。
- 中間成果物: `_tmp/` に出力し、一意名で管理（例: `_tmp/20250115_unsam_draft_01.md`）。PRに `_tmp/` を含めない。
- 日付の決定: connpassで次回「機械学習名古屋研究会」の開催日を確認し、フォルダ日付に使用。
  - サイト取得（推奨）: 検索結果を降順（sort=2）で取得し、_tmpに保存して解析。
    - `mkdir -p _tmp`
    - `curl -fsSL -A 'Mozilla/5.0' 'https://connpass.com/search/?q=機械学習名古屋研究会&select=upcoming&sort=2' -o _tmp/connpass_search_sorted.html`
    - 解析（未来で最も近い日を出力）:
      - `python3 - << 'PY'\nimport re,sys,datetime; from pathlib import Path\nht=Path('_tmp/connpass_search_sorted.html').read_text(errors='ignore')\niso=re.findall(r'(20\\d{2}-\\d{2}-\\d{2}T\\d{2}:\\d{2}:\\d{2}Z)',ht)\njp=re.findall(r'(20\\d{2})/(\\d{1,2})/(\\d{1,2})',ht)\nnow=datetime.datetime.now(datetime.timezone.utc); cand=[]\nfor s in iso:\n  try:cand.append(datetime.datetime.fromisoformat(s.replace('Z','+00:00')))\n  except:pass\nfor y,m,d in jp:\n  try:cand.append(datetime.datetime(int(y),int(m),int(d),tzinfo=datetime.timezone.utc))\n  except:pass\nassert cand,'NO_DATE_FOUND'\nfuture=[c for c in cand if c>=now]; ch=min(future) if future else max(cand)\nprint(ch.strftime('%Y/%m/%d'))\nPY`
  - API（参考）: `curl -s 'https://connpass.com/api/v1/event/?keyword=機械学習名古屋研究会&count=1&order=2' | jq -r .events[0].started_at`
  - シリーズIDが判明している場合は `series_id` を優先（安定）。
  - 取得結果に不確実性がある場合、必ず手動でページを確認。
- 論文取得（環境作成）:
  - `uv venv .venv && source .venv/bin/activate`
  - 必要に応じて取得/解析ツールを導入: `uv pip install arxiv httpx lxml` など。
  - uv が未インストールの場合のフォールバック:
    - `python3 -m venv .venv && . .venv/bin/activate`
    - `pip install -U pip setuptools wheel && pip install arxiv httpx lxml`
    - 判定例: `command -v uv >/dev/null || echo 'uv not found'`
- 要約作成（n-kats準拠）:
  - 先頭3行・見出し順を踏襲。画像は扱えない前提で、想定図のプレースホルダを本文に挿入（例: `![図1 想定: アーキテクチャ図](./<basename>/fig1_placeholder.png)`）。
  - arXiv/PDF から著者名を抽出し、「著者」セクションを3行目の直後に追加。
  - この段階では README.md を作成しない（別PRで作成）。
  - アブストラクトだけでなく、必ず PDF をダウンロードして本文を確認のうえで要約を作成する。
  - 論文全体の利用: 要約作成時は PDF の全文（必要に応じて付録を含む）を根拠として記述する。アブストラクトのみでの作成は禁止。
  - 長文時の事前確認: ページ数がおおむね30ページ以上の論文は、要約着手前に担当者へ確認を取り、範囲・粒度・重点項目を合意してから進める。
  - 想定問答（Q&A）は Markdown の本文には入れない（PR コメント等で別途提示）。

- 最終化・移動（draft → 本番配置）:
  - `_tmp/` で作成した下書きを、決定した開催日フォルダへ「移動」し、ファイル名は `<topic>_<arXivID>.md` とする。
    - 例: `_tmp/20250918_auras_draft_01.md` → `20250918_reports/auras_2509.09560.md`
  - 同名アセットフォルダを日付フォルダ直下に用意（例: `20250918_reports/auras_2509.09560/`）。
  - 注意（過去の誤りの反省）: Markdown をトピック名のサブディレクトリに入れない。
    - 誤: `20250918_reports/auras/auras_2509.09560.md`
    - 正: `20250918_reports/auras_2509.09560.md`
  - 移動後は `_tmp/` 側のドラフトは削除し、重複・乖離を避ける。
- レビュー観点:
  - 日本語の不自然さ・論理飛躍・用語の一貫性を校正。
  - 想定問答はファイル外（コメントやレビュー用メモ）で用意し、本文に含めない。
- 実務上の注意:
  - すべて相対パス。`rg` を優先して調査。大きな変更は小さなコミットに分割。

## list.md の作成・更新手順（ドキュメント）
- 勉強会インデックス `list.md` の更新方法は `docs/how_to_write_list.md` を参照。
  - 回番号の確認、各レポートからのタイトル/リンク/アカウント抽出、ジャンルの付与、重複防止、表形式の記法（同一回の2行目以降は `||` 始まり）などの手順を記載。
  - 中間ファイルは `_tmp/` を使用し、コミットに含めない運用とする。

## 依存コマンドの取得（_cache/bin）
- 原則: 足りないコマンドはリポジトリ直下の`_cache/bin`に配置し、`PATH`を通す。
  - 準備: `mkdir -p _cache/bin && export PATH="$PWD/_cache/bin:$PATH"`
- uv（なければ）:
  - `curl -fsSL https://astral.sh/uv/install.sh | sh -s -- --install-dir _cache/bin`
- jq（なければ, Linux x86_64想定）:
  - `curl -fsSL -o _cache/bin/jq https://github.com/jqlang/jq/releases/latest/download/jq-linux-amd64 && chmod +x _cache/bin/jq`
- ripgrep/rg（なければ, Linux x86_64想定）:
  - `ver=$(curl -fsSL https://api.github.com/repos/BurntSushi/ripgrep/releases/latest | jq -r .tag_name)`
  - `curl -fsSL -o /tmp/rg.tgz https://github.com/BurntSushi/ripgrep/releases/download/$ver/ripgrep-$ver-x86_64-unknown-linux-musl.tar.gz`
  - `tar -xzf /tmp/rg.tgz -C /tmp && mv /tmp/ripgrep-*/rg _cache/bin/rg && chmod +x _cache/bin/rg`
- tree の代替: `find`で代用可能（例: `find 2024* -maxdepth 2 -type d | sed 's|[^/]*/|  |g'`）。
- 注意: `_cache/`はローカル専用。コミットやPRには含めない。

## Codex/MCP 設定（fetch サーバの追加）
- 目的: エージェントがHTTP取得を行えるよう、MCPの`fetch`サーバを有効化。
- 手順:
  1) Nodeがあれば `npx` を使う。なければ `_cache/bin` に Node/npm を用意するか、手動で実行環境を整える。
  2) `.codex/config.example.json` をCodex CLIの設定として利用。
     - リポジトリ直下の`.codex/config.json`を参照するクライアントの場合: 例をコピー
       - `cp .codex/config.example.json .codex/config.json`
     - 別パスの設定を参照するクライアントの場合: 既存設定の`mcpServers`に以下を統合
       - `"fetch": { "command": "npx", "args": ["-y", "@modelcontextprotocol/server-fetch"] }`
  3) 必要に応じて`PATH`に`_cache/bin`を追加。
- 備考: Pythonのみの環境では代替が未整備のため、Node/npm（`npx`）の用意を推奨。

## ユーザー情報の扱い（担当者名）
- 保存場所: `_cache/user.md`（PRやコミットに含めないローカル情報）。
- フォーマット（例）:
  - シンプル: `username: n-kats` の1行のみ。
- 利用箇所: 各要約の3行目 `(まとめ @<username>)` に反映。
- 取得手順:
  - 存在確認して未検出なら、対話で「担当者名（GitHub/ハンドル）を教えてください」と質問し、作成。
  - 作成例: `mkdir -p _cache && printf 'username: %s\n' "<NAME>" > _cache/user.md`
- 注意: `_cache/user.md` はローカル専用（.gitignore 済み）。レビュー/PRでは参照のみで内容は提出しない。
