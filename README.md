# apps-legal

Tomoyuki Kimura が開発する全アプリの規約・ポリシーを管理するリポジトリ。  
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
│   ├── index.html           ← 規約・ポリシーポータル（全アプリ一覧）
│   └── kakugenko/
│       ├── index.html          ← 格言庫ハブ（文書一覧）
│       ├── terms.md            ← 利用規約（Jekyll がHTML化）
│       ├── privacy-policy.md   ← プライバシーポリシー（Jekyll がHTML化）
│       └── contact.html        ← お問い合わせフォーム（Web3Forms）
└── en/
    ├── index.html           ← Developer portal (all apps)
    └── kakugenko/
        ├── index.html          ← KakugenKo hub
        ├── terms.md
        ├── privacy-policy.md
        └── contact.html
```

**ページ階層:**
```
ルート → 規約・ポリシーポータル（アプリ一覧）→ アプリハブ（文書一覧）→ 各文書
```

## アプリからのリンク先

アプリは `getCurrentLocale()` で言語を取得し、動的にURLを構築する。

| 画面 | URL（ja の例） |
|------|--------------|
| 利用規約 | `https://tomoynet.github.io/apps-legal/ja/kakugenko/terms` |
| プライバシーポリシー | `https://tomoynet.github.io/apps-legal/ja/kakugenko/privacy-policy` |
| お問い合わせ | `https://tomoynet.github.io/apps-legal/ja/kakugenko/contact.html` |
| アプリハブ | `https://tomoynet.github.io/apps-legal/ja/kakugenko/` |
| 規約・ポリシーポータル | `https://tomoynet.github.io/apps-legal/ja/` |

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

`kakugenko/` を雛形にしてコピーし、各ファイルでアプリ名・URL を置換する運用。Web3Forms の `access_key` は全アプリ共通で使い回す（Web3Forms 管理画面では `subject` で振り分けて確認する）。

### 手順

1. `ja/新アプリ名/` と `en/新アプリ名/` を作成し、以下を配置する

```
ja/新アプリ名/
├── index.html          ← アプリハブ（kakugenko/index.html を参考に作成）
├── terms.md            ← フロントマターの app_name 等を変更
├── privacy-policy.md
└── contact.html
```

2. `ja/index.html` と `en/index.html`（規約・ポリシーポータル）にアプリのカードを追記する

### 各ファイルで書き換える箇所（チェックリスト）

新アプリを追加するときに漏れやすい項目。kakugenko を雛形にコピーした後、以下をすべて更新する。

**`<app>/index.html`（アプリハブ）**
- `<title>` のアプリ名
- `<h1>` のアプリ名
- `<p class="subtitle">` のアプリ名

**`<app>/terms.md` / `<app>/privacy-policy.md`（フロントマター）**
- `title` のアプリ名（例: `利用規約 - 新アプリ名`）
- `app_name`
- `back_label`（例: `← 新アプリ名`）
- `lang_alt_url`（ja↔en の対応パス。コピペミスで 404 を踏みやすいので注意）
- `updated`（制定日・最終更新日）

**`<app>/contact.html`**
- `<title>` / `<h1>` / `<p class="subtitle">` のアプリ名
- back link の `← アプリ名`
- `<input name="from_name">` の value（例: `新アプリ名 お問い合わせ`）
- `<input name="subject">` の value（例: `【新アプリ名】お問い合わせ`）
- `<input name="access_key">` は **kakugenko と同じ値のままで OK**（共通キー）

**ルートの `ja/index.html` / `en/index.html`（規約・ポリシーポータル）**
- `<ul class="doc-list">` 内に新しい `<li>` カードを追記
- `href="./新アプリ名/"` とアプリ名・説明文

## 開発者

Tomoyuki Kimura
