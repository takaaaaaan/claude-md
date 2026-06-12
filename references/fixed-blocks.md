# A ブロック逐語テキスト

`claude-md-init` / `claude-md-align` が CLAUDE.md に **そのまま貼り込む** 固定セクション。`<...>` のプレースホルダだけ、検出値で置き換える。順番・位置は [`format.md`](./format.md) の骨格に従う。

---

## セクション 0 — 冒頭の一文

```markdown
# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.
```

---

## セクション 1 — メンテナンス方針

```markdown
## 重要: このファイルのメンテナンス方針

- このリポジトリで開発が進み、**全体構造やフローが変わった**、または **CLAUDE.md に書かれている内容と実態がズレた**ことに気づいたら、CLAUDE.md を更新する。
- ただし **CLAUDE.md の変更は必ず user の許可を取ってから行うこと**。Claude 側の判断で勝手に書き換えない。「○○の節を××のように更新したい(理由: …)」と提案 → user の "OK" を待ってから編集する。
```

---

## セクション 4 — 作業ルール: worktree とポート（必須）

`<DEFAULT_PORTS>` と `<PORT_RANGE>` は解析で検出した実値に置換する（例: FE なら `3000` / `3100,3200…`、FastAPI BE なら `20000`（docker host マッピング）/ `20000–21000`）。複数サービスがあれば各々について書く。

```markdown
## 作業ルール: worktree とポート（必須）

修正・新機能・実験など **コードに手を入れる作業は、必ず git worktree を切ってから** 進める。メインの作業ツリーで直接いじらない。完了後に ff-merge で戻す。

各 worktree でアプリ/サーバを起動してテストするときは、**他の worktree やデフォルト設定と衝突しないポートを一時的に使う**：

- **デフォルトポート（<DEFAULT_PORTS>）は使わない。** 予約レンジ <PORT_RANGE> 内の別ポート（例: …）を一時的に使う。
- worktree ごとに番号帯を分けて、複数 worktree を同時に立てても衝突しないようにする。

起動したら **user が確認しやすいように URL を提案して伝える**（例: 「http://localhost:XXXX で起動しました。確認してください」）。

**テストが終わったら、起動したプロセス（dev サーバ / uvicorn / docker compose / streamlit など）は必ず停止する。** 立てっぱなしにしてポートを占有しない（`docker compose down` 等）。
```

---

## セクション 9 — Commit style

```markdown
## Commit style（strictly enforced）

`<emoji> <type>: <description>` 形式。**コミットメッセージは韓国語で書く**(インフラ・config 系のみ英語可)。

Types: `✨ feat` `🐛 fix` `♻️ refactor` `🧪 test` `📝 docs` `🔧 chore` `🚀 perf` `💄 style` `🔒 security` `🗑️ remove` `🚧 wip`。

`git add -A` / `git add .` は禁止 — パスを明示してステージする。サブモジュールがある場合は先にサブモジュール内でコミットし、親リポではポインタ更新を別コミットにする。
```
