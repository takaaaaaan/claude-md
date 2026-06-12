# claude-md

CLAUDE.md を **あなたの流儀（house style）** で生成・整形する個人用スキル群。2 つのスキルを 1 リポジトリに収め、形式の定義は `references/` の 1 箇所で共有する（二重管理しない）。

形式の正本は `metabolic-twin-be` / `metabolic-twin-fe` の CLAUDE.md から抽出した、固定セクション（メンテナンス方針・worktree とポート必須ルール・韓国語コミット規約）＋コードベース由来セクションの骨格。

## 2 つのスキル

| スキル | 用途 | トリガ例 |
|---|---|---|
| **`claude-md-init`** | CLAUDE.md が無いリポで、コードベースを解析してゼロから生成（`/init` 相当） | 「CLAUDE.md を作って」「init して」 |
| **`claude-md-align`** | 既存 CLAUDE.md を**保全しつつ**流儀の骨格へ整える（提案 → 承認 → 適用） | 「CLAUDE.md を流儀に合わせて」「整えて」 |

## 構成

```
claude-md/
├── .claude-plugin/{plugin.json, marketplace.json}
├── references/
│   ├── format.md         # 正規セクション骨格(A/B/C)＋解析チェックリスト ← 唯一の正本
│   └── fixed-blocks.md   # A 固定セクションの逐語テキスト
└── skills/
    ├── claude-md-init/SKILL.md
    └── claude-md-align/SKILL.md
```

骨格を変えたいときは `references/format.md` を、固定文言を変えたいときは `references/fixed-blocks.md` を直す。両スキルがこれを参照するので、片方だけ直せば両方に効く。

## インストール

```
/plugin marketplace add takaaaaaan/claude-md
/plugin install claude-md@claude-md
```

> `npx skills add` (skills.sh CLI) はリポジトリ直下の単一 `SKILL.md` 前提のため、2 スキル構成のこのリポはプラグイン経由のインストールを使う。

## セクション骨格（A 固定 / B 生成 / C 条件付き）

0. 冒頭の一文 — **A**
1. メンテナンス方針 — **A**
2. 協働とコミュニケーション（報連相） — **A**
3. プロジェクト概要 / 位置づけ — **B**
4. よく使うコマンド — **B**
5. 作業ルール: worktree とポート（必須） — **A**（ポート番号のみ B）
6. ハイレベル構成 — **B**
7. アーキテクチャ — **B**
8. 編集・拡張時の指針 — **B**
9. ドキュメント — **B**
10. Commit style — **A**
11. ファイル変更時のコメント規約 — **A**
12. 姉妹 / 関連リポ説明 — **C**

詳細は `references/format.md` 参照。
