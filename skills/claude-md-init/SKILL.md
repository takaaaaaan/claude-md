---
name: claude-md-init
description: |
  Use when a repository has NO CLAUDE.md and you need to create one from
  scratch in the user's house style by analyzing the codebase — triggered by
  「CLAUDE.md を作って」「CLAUDE.md がない」「/init 相当で」, or onboarding a new
  project/repo. Generates a Japanese CLAUDE.md with the user's fixed
  conventions (worktree+port rules, Korean-commit style, maintenance policy)
  plus codebase-derived sections. NOT for editing an existing CLAUDE.md — use
  claude-md-align for that.
---

# claude-md-init — 流儀準拠の CLAUDE.md を新規生成

新規 / CLAUDE.md 未整備のリポジトリを `/init` の要領で解析し、**あなたの流儀**に沿った CLAUDE.md をゼロから書き起こす。

## 最初に必ず読む

- 形式の正本: **`references/format.md`**（セクション骨格 A/B/C と解析チェックリスト）
- 逐語テキスト: **`references/fixed-blocks.md`**（A 固定セクションの貼り込み文）

この 2 つを読まずに本文を書き始めない。骨格・順番はここに従う。

## 前提チェック

1. 対象リポに `CLAUDE.md` が **無い**ことを確認する。**有れば中止**して `claude-md-align`（整える側）を案内する。上書き生成はしない。
2. リポジトリのルートを確定する（複数リポが並ぶ作業ディレクトリなら対象を user に確認）。

## 手順

1. **解析** — `format.md` の「解析チェックリスト」を上から実行：スタック検出 → コマンド抽出 → ポート検出 → ディレクトリ構成 → アーキテクチャの核 → 拡張指針 → 姉妹リポ判定。
2. **B セクションを生成** — 解析結果だけで概要 / コマンド / 構成 / アーキテクチャ / 拡張指針 / ドキュメントを書く。**確認できない事実は書かない**（コマンド・ポート・ファイルの捏造禁止）。不明点は user に質問するか `<!-- TODO: 要確認 -->` を残す。
3. **A セクションを貼る** — `fixed-blocks.md` の逐語をそのまま挿入。worktree 節の `<DEFAULT_PORTS>` / `<PORT_RANGE>` は解析した実ポートで置換（検出できなければ user に確認）。
4. **C を判定** — 姉妹/関連リポがあればセクション 12 を追加（相手の構造を Q&A 形式で要約）。無ければ省く。
5. **ドラフト提示** — 完成稿を user に見せ、**OK を得てから** `CLAUDE.md` を書き出す（メンテナンス方針と同じく、勝手に確定しない）。
6. **CLAUDE.local.md（任意）** — CLAUDE.md を確定したら、**AskUserQuestion で「個人ローカル専用の CLAUDE.local.md も作るか」を確認**する。作る場合だけ `fixed-blocks.md` の「CLAUDE.local.md テンプレ」で生成し（検出できたローカルポートは穴埋め可）、`.gitignore` に `CLAUDE.local.md` を登録する（未登録なら追記を提案、既にあれば触らない）。要らなければスキップ。
7. コミットするなら Commit style（韓国語・`git add -A` 禁止・パス明示）に従う。**`CLAUDE.local.md` はコミットしない**（`.gitignore` 済み）。

## やらないこと

- 既存 CLAUDE.md の上書き（→ `claude-md-align`）。
- 解析で裏が取れない記述の創作。
- user の OK を待たずにファイルを確定すること。
- user に確認せず CLAUDE.local.md を勝手に作る、または共有すべき内容を CLAUDE.local.md 側に逃がすこと。
