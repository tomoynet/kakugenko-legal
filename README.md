# apps-legal

Tomoyuki Kimura が開発するアプリの法的文書を管理するリポジトリ。  
GitHub Pages + Jekyll で公開される。

公開URL: `https://tomoynet.github.io/apps-legal/`

---

## ディレクトリ構造

```
apps-legal/
├── _config.yml              ← Jekyll設定
├── _layouts/
│   └── legal.html           ← MDコンテンツページ共通レイアウト
├── assets/
│   └── style.css            ← 共通スタイルシート
├── index.html               ← ルート（navigator.language で ja/en に自動リダイレクト）
├── ja/
│   ├── index.html           ← 日本語ポータル
│   └── kakugenko/
│       ├── privacy-policy.md   ← プライバシーポリシー（Jekyll がHTML化）
│       ├── terms.md            ← 利用規約（Jekyll がHTML化）
│       └── contact.html        ← お問い合わせフォーム（Web3Forms）
└── en/
    ├── index.html           ← English portal
    └── kakugenko/
        ├── privacy-policy.md
        ├── terms.md
        └── contact.html
```

## アプリからのリンク先

アプリは `getCurrentLocale()` で言語を取得し、動的にURLを構築する。

| 画面 | URL（ja の例） |
|------|--------------|
| プライバシーポリシー | `https://tomoynet.github.io/apps-legal/ja/kakugenko/privacy-policy` |
| 利用規約 | `https://tomoynet.github.io/apps-legal/ja/kakugenko/terms` |
| お問い合わせ | `https://tomoynet.github.io/apps-legal/ja/kakugenko/contact.html` |
| ポータル | `https://tomoynet.github.io/apps-legal/ja/` |

## お問い合わせフォームの設定

`ja/kakugenko/contact.html` および `en/kakugenko/contact.html` の以下の箇所に Web3Forms の Access Key を設定する。

```html
<input type="hidden" name="access_key" value="YOUR_WEB3FORMS_ACCESS_KEY">
```

Access Key は [Web3Forms](https://web3forms.com/) で取得する。

## MDファイルの更新方法

1. 対象の `.md` ファイルを編集（フロントマターの `updated:` も更新）
2. GitHub にプッシュすると Jekyll が自動でHTMLに変換して公開される

## 新しいアプリを追加するとき

```
ja/
└── 新アプリ名/
    ├── privacy-policy.md   ← フロントマターの app_name などを変更
    ├── terms.md
    └── contact.html
```

`ja/index.html` および `en/index.html` のポータルにリンクを追記する。

## 開発者

Tomoyuki Kimura
