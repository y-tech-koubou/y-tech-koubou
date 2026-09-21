# 設定画面のブランド署名コンポーネント

各アプリの設定画面（最下部）に共通配置する「Yテック工房」ブランド署名のデザイン仕様。

---

## 目的

- 利用者にプロダクト群が同じ作者の手によるものだと自然に伝える
- 他のYテック工房製品への導線を控えめに提示する
- ブランド帰属感を強くしすぎず、プロダクト体験を阻害しない

---

## レイアウト

設定画面のリスト末尾、フッター位置に配置する。

```
┌─────────────────────────┐
│  設定                    │
├─────────────────────────┤
│  ○ 通知設定              │
│  ○ テーマ                │
│  ○ データ管理            │
│  ○ プライバシー          │
│  ○ アプリ情報            │
│                         │
│  ─────────────────       │ ← 区切り線（薄墨 #DAD6CF）
│                         │
│        [マーク]          │ ← ロゴマーク 40×40
│      Yテック工房         │ ← Noto Serif JP 14px
│      Y-TECH KOUBOU      │ ← Cormorant Garamond 10px
│                         │
│   他のプロダクトを見る →   │ ← TouchableOpacity（小）
│                         │
│      v1.0.0 (2026)      │ ← バージョン表記
└─────────────────────────┘
```

---

## 寸法仕様

| 要素 | 仕様 |
|---|---|
| 上の区切り線 | 1px solid `#DAD6CF`、上下に余白24px |
| ロゴマーク | 40 × 40px、横中央 |
| ブランド名（和文） | Noto Serif JP Medium 14px、色 `#282950`（ダーク時 `#F7F5F2`） |
| ブランド英名 | Cormorant Garamond Medium 10px、色 `#5E646B`、letter-spacing 0.3em |
| 「他のプロダクトを見る」 | Noto Sans JP Regular 12px、色 `#5E646B`、上下12pxパディング |
| バージョン表記 | Noto Sans JP Regular 10px、色 `#6B7280` |
| 全体縦サイズ | 約140px |

---

## React Native 実装サンプル

```tsx
import { View, Text, TouchableOpacity, Image, Linking, StyleSheet } from 'react-native';

export function BrandSignature({ version }: { version: string }) {
  const handlePress = () => {
    Linking.openURL('https://y-tech-koubou.com');
  };

  return (
    <View style={styles.container}>
      <View style={styles.divider} />
      <Image
        source={require('../assets/brand/logo-mark.png')}
        style={styles.mark}
      />
      <Text style={styles.brandJp}>Yテック工房</Text>
      <Text style={styles.brandEn}>Y-TECH KOUBOU</Text>
      <TouchableOpacity onPress={handlePress} hitSlop={8}>
        <Text style={styles.link}>他のプロダクトを見る →</Text>
      </TouchableOpacity>
      <Text style={styles.version}>v{version}</Text>
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    alignItems: 'center',
    paddingVertical: 32,
    paddingHorizontal: 24,
  },
  divider: {
    width: '60%',
    height: 1,
    backgroundColor: '#DAD6CF',
    marginBottom: 24,
  },
  mark: {
    width: 40,
    height: 40,
    marginBottom: 12,
  },
  brandJp: {
    fontFamily: 'NotoSerifJP-Medium',
    fontSize: 14,
    color: '#282950',
    letterSpacing: 1.2,
  },
  brandEn: {
    fontFamily: 'CormorantGaramond-Medium',
    fontSize: 10,
    color: '#5E646B',
    letterSpacing: 3,
    marginTop: 2,
  },
  link: {
    fontFamily: 'NotoSansJP-Regular',
    fontSize: 12,
    color: '#5E646B',
    marginTop: 16,
    paddingVertical: 4,
  },
  version: {
    fontFamily: 'NotoSansJP-Regular',
    fontSize: 10,
    color: '#6B7280',
    marginTop: 12,
  },
});
```

---

## 配置箇所

| アプリ | 配置先ファイル |
|---|---|
| architect-quiz | `app/settings.tsx` or `app/manage.tsx` の末尾 |
| koji-app | `app/(tabs)/settings.tsx` |
| invest-ai | `app/settings/index.tsx` |
| africa-map | `app/settings.tsx` |

---

## ダークモード対応

すべての色を BRAND.md の対応色に切り替える。
区切り線は `#3A4A3A`（薄墨のダーク版）に変更。

---

## アクセシビリティ

- `accessibilityRole="link"` をリンク部分に付与
- ロゴマークに `accessibilityLabel="Yテック工房ロゴ"`
- リンクテキストに `accessibilityLabel="Yテック工房の他のプロダクトを見る"`
- タップ領域は最低44 × 44px確保（hitSlop で拡張）

---

## A/B テスト候補

将来的に検証する余地のあるバリエーション:

1. リンクの文言「他のプロダクトを見る」vs「Yテック工房について」vs「公式サイト」
2. ロゴマークの有無
3. プロダクト一覧をその場で展開するアコーディオン形式

初期実装は本仕様書のまま。検証は実装後3ヶ月以上経過してから。
