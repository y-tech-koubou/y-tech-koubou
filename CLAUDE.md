# CLAUDE.md — y-tech-koubou (ブランド／ポータル)

このリポジトリは Yテック工房のブランド正本とポータルサイトを管理する。

## 最重要ルール: BRAND.md が正本

- **`BRAND.md` がブランドの Source of Truth。** ポータル(`portal/index.html`)・ストア掲載・SNS・名刺はすべてこの下流。
- **ブランド軸（タグライン／コンセプト／3つの柱／メール署名／ハッシュタグ）を変えるときは、ポータルだけ直して終わらせない。同じ作業の中で必ず `BRAND.md` も更新する。**
- ポータルで古い表現の「取り残し」を見つけたら、正本との差分を疑い、両方を揃える。
- ブランド変更のコミットは `BRAND: ...` プレフィックスを付ける。

### 現行ブランド軸（2026-06-04 時点）

- タグライン: **IT × 建築 × 海外** / IT × Architecture × Overseas
- 3つの柱: 01 IT（IT で形にする）／02 Architecture（建築のまなざし）／03 Global（海外の視点）
- 旧軸「種から育てる工房」「建築 × IT × 暮らし」「建築 × IT × 国際協力」は**廃止**。残っていたら直す。

### 【厳守】事実表現

- 主宰は一級建築士の**有資格者ではない（受験中）**。「一級建築士」「建築士」など**有資格と読める表現は全面禁止**。
- 正しい言い回し: 「建築を学ぶ視点」「建築のまなざし」。

## ブランド変更時の整合チェック

ブランド軸を変えたら、以下が全部同じ言葉か確認する（詳細は BRAND.md §12）:

1. `portal/index.html` の `<title>` / `meta description` / `og:*` / `twitter:*` / JSON-LD `description`
2. ヒーローのタグライン（`.hero-tag`）
3. About のリード文と3つの柱
4. フッターのタグライン
5. `BRAND.md`（§1 / §3 / §10 / §11）
6. **画像資産**: `portal/assets/og.png` に焼き込まれたタグライン（再生成は `og-source.html` をEdgeヘッドレスで1200×630スクショ→ `?v=` バンプ）。2026-06-05 に旧軸が画像だけ残る取り残しが実際に起きた

## デプロイ

ポータルは Git 連携なし。手動で本番反映する:

```powershell
cd C:\Users\yoshino.takayuki\y-tech-koubou\portal
npx vercel --prod
```

## デザイン指針
- **ブランド文言・事実表現は BRAND.md が正本（このセクションより優先）。** 以下はビジュアル数値の参照
- **現行ビジュアル＝Heritage Design Tokens（2026-06-23 採用・本番反映済）**。"Architectural Minimalism meets Journalistic Gravitas"。`portal/index.html` の `:root` がトークン正本（変数名は据え置き＝下流無改修で色を拾う設計）。
  - 配色: アクセント=Accent Blue `#2563EB`（唯一のアクセント＝旧 `--kokemidori` を上書き。2026-07-11に旧Boston Clay `#B8422E` から変更）／地=Limestone `#F7F5F2`（`--kinari`）／文字=Ink `#1A1C1E`（`--shikkoku`）／補足=Slate `#5E646B`（`--nibiiro`）。**旧:苔緑×生成りの和風パレットは廃止。緑(#2D5A2D等)を復活させない。**
  - **見出し(h2/h3等)・kicker・カード名・.mono/.idxバッジにAccentを使わない＝Ink/Slate固定**（2026-07-11是正。それまで`section h2`等がAccentを流用しアクセント色変更のたびに見出しごと色が変わる実装ミスだった。`--heading-clay`系トークンはInk/Slateへのエイリアスとして`portal/index.html`の`:root`に残置＝下流セレクタは無改修）。
  - 書体: 見出し/本文=Public Sans＋日本語Noto Sans JP（`--serif-jp`/`--sans-jp`）／ラベル(uppercase caps)=Space Grotesk（`--serif-en`）。
  - 例外: **ヒーローの木のキャンバスアート＋種ロゴは緑のまま据え置き**（2色試作のうえ緑を維持と決定・木は有機的シグネチャ）。木の葉色を勝手にクレイ/モノクロ化しない。
- 旧参照（記録）: 正本 `design-system\DESIGN-SYSTEM.md`＋`DESIGN-LIBRARY.md`（70ブランド索引）／参照ブランド linear, vercel, claude。引く要素: 静かな技術感・mono eyebrow・「IT×建築×海外」の編集性。
