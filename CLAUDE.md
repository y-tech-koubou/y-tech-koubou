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
- 正本: `C:\Users\yoshino.takayuki\design-system\DESIGN-SYSTEM.md`（規律）＋ `design-system\DESIGN-LIBRARY.md`（70ブランド索引）
- 参照ブランド: 第一= **linear, vercel** / 補助= claude（フルMD= `Desktop\Yテック工房\デザイン\DESIGN-<brand>.md`）。引く要素: 静かな技術感・mono eyebrow・「IT×建築×海外」の編集性
