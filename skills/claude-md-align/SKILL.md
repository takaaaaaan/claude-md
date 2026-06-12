---
name: claude-md-align
description: |
  Use when a repository ALREADY has a CLAUDE.md and the user wants it brought
  into their house style / format — triggered by 「CLAUDE.md を流儀に合わせて」
  「整えて」「揃えて」「この形式に直して」. Preserves existing hand-written content,
  supplements missing fixed sections (worktree+port, Korean-commit style,
  maintenance policy), and reorders to the canonical skeleton — proposing
  changes for approval before writing. NOT for creating a CLAUDE.md from
  scratch — use claude-md-init for that.
---

# claude-md-align — 既存 CLAUDE.md を流儀に寄せる（保全＋提案型）

既存の CLAUDE.md を捨てずに、**あなたの流儀の骨格**へ整える。中身は最大限保全し、足りない固定セクションを補い、順番を揃える。

## 最初に必ず読む

- 形式の正本: **`references/format.md`**（セクション骨格 A/B/C）
- 逐語テキスト: **`references/fixed-blocks.md`**（A 固定セクションの貼り込み文）

## 中核原則: 保全＋提案

- **B 生成セクション**（概要・コマンド・構成・アーキテクチャ・拡張指針・ドキュメント）の **手書きの中身は保持する**。明確な実態ズレや空欄だけ直す。勝手に書き直さない。
- **A 固定セクション**（メンテナンス方針 / worktree とポート / Commit style）が欠けていれば `fixed-blocks.md` から補う。既にあれば逐語と突き合わせて差分だけ提案。
- 順番を `format.md` の骨格に並べ替える。
- **書き換える前に必ず提案**して user の OK を待つ — これは対象リポのメンテナンス方針（「変更は必ず user 許可」）とも一致する。

## 手順

1. 既存 `CLAUDE.md` を読む。**無ければ中止**して `claude-md-init` を案内。
2. 既存の各セクションを骨格の #0〜#10 に **マッピング**する（どれが A/B/C のどこに当たるか）。
3. 差分を洗い出す：
   - **欠けている A セクション**（補う対象）
   - **保全する B の中身**（触らない範囲）
   - **実態ズレ / 空欄**（コードベースを確認して直す候補）
   - **並べ替え**（移動するセクション）
4. **提案を提示** — 「追加 / 移動 / 修正したい箇所」と各理由を箇条書きで user に見せる。差分が分かる形で。
5. **OK を得たぶんだけ適用** して `CLAUDE.md` を書き出す。却下された変更は入れない。
6. コミットするなら Commit style に従う。

## やらないこと

- ゼロからの全面再生成（手書きのニュアンスを失う。新規は `claude-md-init`）。
- 既存 B セクションの無断書き換え。
- user の承認を待たずに保存すること。
