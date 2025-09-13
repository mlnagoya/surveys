# Repository Guidelines

## プロジェクト構成
- レポートは日付ごとのフォルダ: `YYYYMMDD_reports/<topic>/`。
- 各 Markdown と同名のアセット用フォルダを併設: 例) `UnSAM_2406.20081.md` と `UnSAM_2406.20081/`。
- 画像は相対パスで参照: `![説明](./<md_basename>/image.png)`。
  例: `20240516_reports/idefics2_2405.02246/fromage.png`。

## ビルド・プレビュー・開発
- ビルドは不要。任意のエディタ/ビューアで Markdown を開いて確認。
- 便利なコマンド例:
  - レポート一覧: `find . -maxdepth 2 -type d -name '*_reports'`
  - 文字列検索: `rg -n "keyword" 2024* 2023* 2022*`
  - ツリー表示: `tree -L 2 2024*`（`tree` がある場合）



## スタイルと命名規約（n-kats 準拠）
- 先頭3行の書式:
  1) H1 に論文タイトル  2) arXiv URL  3) `(まとめ @github_id)`。
- 見出しの順序（例）:
  `# どんなもの？` → `# 先行研究と比べてどこがすごい？` → `# 技術や手法の肝は？` →
  `# どうやって有効だと検証した？` → `# 議論はある？` → `## 私見` → `# 次に読むべき論文は？`。
- 命名:
  - Markdown: `<Topic>_<arXivID>.md`（例: `idefics2_2405.02246.md`）。
  - 画像フォルダ: `<Topic>_<arXivID>/` に配置（例: `./idefics2_2405.02246/arch.png`）。
  - 画像名: `snake_case.ext`、サイズは概ね < 2 MB。
-
  - 1ファイル1つの H1。箇条書きを優先、1行は約100文字目安。

## テスト/品質確認
- 各レポートで手動確認:
  - 画像が表示される（相対パスのみ）。
  - 参照リンクが解決する。外部直リンクは極力避ける。
  - 大文字小文字の不一致がない。
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
  - この段階では README.md を作成しない（別PRで作成）。
- レビュー観点:
  - 日本語の不自然さ・論理飛躍・用語の一貫性を校正。
  - 想定問答を3–5項目列挙（再現性、比較対象、計算資源、制約、拡張性など）。
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
- 保存場所: `_tmp/user.md`（PRやコミットに含めないローカル情報）。
- フォーマット（例）:
  - シンプル: `username: n-kats` の1行のみ。
- 利用箇所: 各要約の3行目 `(まとめ @<username>)` に反映。
- 取得手順:
  - 存在確認して未検出なら、対話で「担当者名（GitHub/ハンドル）を教えてください」と質問し、作成。
  - 作成例: `mkdir -p _tmp && printf 'username: %s\n' "<NAME>" > _tmp/user.md`
- 注意: `_tmp/user.md` は共有しない。レビュー/PRでは参照のみで内容は提出しない。
