# 設計メモ: claude-md スキル群（2026-06-11）

## 目的

`metabolic-twin-be` / `metabolic-twin-fe` の CLAUDE.md に共通する「自分の流儀」を抽出し、別プロジェクトでも再利用できるスキルにする。

- 既存 CLAUDE.md を流儀に合わせて整える（**align**）
- 新規プロジェクトで流儀準拠の CLAUDE.md を作る（**init**、`/init` 相当）

## 決定事項（ブレインストーミングの回答）

| 論点 | 決定 |
|---|---|
| 対象 | **自分専用**。個人規約（日本語散文・韓国語コミット・worktree/ポート必須・emoji type 一覧・メンテ方針）をスキルに固定で焼き込む |
| コマンド構成 | **2 スキルに分ける**（init / align）。実装は 1 リポジトリ内 2 スキルで共有 references を 1 箇所に |
| セクション骨格 | A 固定 / B 生成 / C 条件付き の骨格でOK |
| align の挙動 | **保全＋提案型**。既存の中身を保持、欠けた固定節を補い、順番を揃え、書き換え前に提案 → user OK |

## 形式の核（2 ファイルの共通点）

固定（A）: メンテナンス方針、worktree とポート必須ルール、Commit style（韓国語）。
生成（B）: 概要 / コマンド / 構成 / アーキテクチャ / 拡張指針 / ドキュメント。
条件付き（C）: 姉妹リポ説明（FE↔BE のような相互参照）。

## 成果物

```
claude-md/
├── .claude-plugin/{plugin.json, marketplace.json}
├── README.md
├── docs/2026-06-11-claude-md-skills-design.md  ← このファイル
├── references/{format.md, fixed-blocks.md}     ← 共有の正本
└── skills/{claude-md-init,claude-md-align}/SKILL.md
```

## 設計上の要点

- **二重管理回避**: 形式の定義は `references/` に 1 セットだけ。両スキルが参照する。
- **捏造禁止**: init は解析で裏が取れない記述を書かない。不明は質問か TODO。
- **承認ゲート**: init も align も、ファイル確定前に必ず user の OK を取る（メンテナンス方針と整合）。
- **skills.sh 制約**: 単一 SKILL.md 前提のため、2 スキル構成はプラグイン経由インストール想定。
