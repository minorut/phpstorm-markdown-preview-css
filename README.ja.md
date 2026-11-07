# phpstorm-markdown-preview-css

[English](README.md) | 日本語

PhpStorm の Markdown プレビューを GitHub 風の見た目にするための CSS です。VS Code のプレビューでも使えます。

[sindresorhus/github-markdown-css](https://github.com/sindresorhus/github-markdown-css) v5.9.0 のライト版とダーク版を元にしています。

| ファイル | テーマ |
|---|---|
| `github-markdown-dark.css` | ダーク |
| `github-markdown-light.css` | ライト |

OS やエディタのテーマで自動的に切り替わることはありません。使いたい方のファイルを指定してください。

## 使い方

### PhpStorm

1. `github-markdown-light.css`（または `github-markdown-dark.css`）を、プレビューを使うプロジェクトの中にダウンロードする（プロジェクトの外にあるファイルは読み込まれません）

   ```sh
   curl -LO https://raw.githubusercontent.com/minorut/phpstorm-markdown-preview-css/main/github-markdown-light.css
   ```

2. Settings（macOS では Settings / Preferences）を開く
3. **Languages & Frameworks → Markdown** を開く
4. **Custom CSS** の **Load from** にチェックを入れ、ダウンロードしたファイルのパスを指定する

### VS Code

> [!NOTE]
> 作者は PhpStorm ユーザーのため、VS Code での表示は簡単な確認にとどめています。崩れている箇所があれば Issue などで教えてください。

`settings.json` の `markdown.styles` に CSS のパスか URL を指定します。パスで指定する場合は、開いているワークスペースの中にあるファイルを指定してください（ワークスペースの外にあるファイルは読み込まれません）。

```json
{
  "markdown.styles": [
    "https://cdn.jsdelivr.net/gh/minorut/phpstorm-markdown-preview-css@main/github-markdown-light.css"
  ]
}
```

## 元の CSS からの変更点

セレクタの `.markdown-body` を `body` に置き換えました。エディタのプレビューには `.markdown-body` 要素がないためです。

そのうえで、各ファイル末尾の `Customizations` セクションに次の上書きを追加しています。

### 共通（ライト・ダーク）

- github-markdown-css が推奨するページレイアウト（最大幅 980px、余白）

### PhpStorm 向け

- PhpStorm の組み込みスタイル（default.css）にあって GitHub にないものを打ち消す
  - 見出し（h1〜h3）の上の余白（ライト・ダーク）
  - 引用ブロックの角丸（ライト・ダーク）
  - リンク色（ライトのみ）
- エディタのダークテーマが当てる背景色・文字色を打ち消す（ライトのみ）

### VS Code 向け（ライト・ダーク）

- 表・見出し（h1, h2）・水平線の罫線の色を打ち消す
- コードブロックに付く枠線を打ち消す
- エディタの背景色を使うスクロールバーの色を打ち消す

## カスタマイズ

各ファイル末尾の `/* ===== Customizations ===== */` より下に、自分のスタイルを書いてください。元の部分は書き換えないでおくと、上流の更新を取り込みやすくなります。

## 上流の更新を取り込む

1. 最新の CSS を取得し、`.markdown-body` を `body` に置き換える

   ```sh
   for t in light dark; do
     curl -sL "https://unpkg.com/github-markdown-css/github-markdown-$t.css" \
       | sed 's/\.markdown-body/body/g' > "/tmp/upstream-$t.css"
   done
   ```

2. 各ファイルの、先頭コメントと `Customizations` セクションのあいだを、取得した内容で置き換える
3. 先頭コメントのバージョン番号を更新する

## ライセンス

MIT License。元の著作権表示は [LICENSE](LICENSE) と各 CSS の先頭コメントに残しています。
