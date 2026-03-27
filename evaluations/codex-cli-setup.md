# OpenAI Codex CLI 導入・使い方

調査日: 2026-03-28

## 概要

OpenAI の Codex CLI は Claude Code のバックアップとして導入。ChatGPT Plus ($20/月) で認証し、gpt-5.4 モデルで動作する。

## 前提条件

| 項目 | 内容 |
|---|---|
| 認証方式 | ChatGPT Plus / Pro サブスクリプション（`codex login`）または OpenAI API キー |
| モデル | gpt-5.4（デフォルト） |
| Node.js | 必須 |

## インストール

```bash
npm install -g @openai/codex
codex login  # ChatGPT アカウントでログイン
```

## 設定ファイル構成

```
~/.codex/
├── config.toml       # MCP・プロファイル・マルチエージェント設定
├── AGENTS.md         # グローバル指示（Claude Code の CLAUDE.md 相当）
└── agents/
    ├── explorer.toml       # 読み取り専用調査エージェント
    ├── reviewer.toml       # レビューエージェント
    └── docs-researcher.toml # ドキュメント調査エージェント
```

## 基本操作

| 操作 | 方法 |
|---|---|
| 起動 | `codex` |
| 終了 | `q` または `Ctrl+C` |
| モデル変更 | `/model` |
| エージェント確認 | `/agent` |
| スキル一覧 | `/skills` |
| 承認 / 拒否 | `y` / `n` |

## プロファイル

```bash
codex -p strict   # 読み取り専用・承認必須
codex -p yolo     # 承認なしで全自動
```

## 有効な MCP サーバー（デフォルト）

| MCP | 用途 |
|---|---|
| GitHub | リポジトリ操作 |
| Context7 | ライブラリドキュメント参照 |
| Exa | Web 検索 |
| Memory | セッション間記憶 |
| Playwright | ブラウザ操作 |
| Sequential Thinking | 複雑な推論 |

## Claude Code との違い

| 機能 | Claude Code | Codex CLI |
|---|---|---|
| 設定ファイル | `CLAUDE.md` | `AGENTS.md` |
| スラッシュコマンド | 豊富（スキル等） | ほぼ instruction ベース |
| フック | あり（8種） | **なし** |
| MCP | フル対応 | `config.toml` で設定 |
| モデル | Claude | gpt-5.4 |
| マルチエージェント | Task ツール | `/agent` + `[agents.<name>]` |

## 用途

Claude Code のトークン上限に達したときのバックアップとして使用。
