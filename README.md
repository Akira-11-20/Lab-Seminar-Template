# 輪講資料テンプレート

研究室の輪講資料用のTypstテンプレートです。設定ファイルベースで、簡単にカスタマイズできます。

## ファイル構成

```
labseminar_template/
├── config.typ         # 設定ファイル（マージン、フォントなど）
├── template.typ       # テンプレート本体
├── main.typ           # サンプル文書（メインファイル）
├── references.bib     # 参考文献ファイル
├── Figures/           # 画像ファイル用ディレクトリ
│   ├── typst.svg
└── README.md          # このファイル
```

## 使い方

### 1. 基本的な使い方

`main.typ`を参考に、新しいファイルを作成します：

```typst
#import "template.typ": rinko, emphasis-box, warning-box, bordered-box

#show: rinko.with(
  title: "あなたの資料タイトル",
  author: "あなたの名前",
  affiliation: "○○研究室 輪講資料",
  // date: (2025, 10, 19), // 指定しない場合は今日の日付
)

= はじめに

本文をここに書く...
```

### 2. コンパイル

```bash
cd labseminar_template
typst compile main.typ
```

または：

```bash
typst compile main.typ output.pdf
```

### 3. 設定のカスタマイズ

`config.typ`を編集することで、全体の設定を変更できます。

## 主な機能

### 自動ヘッダー・フッター

- **ヘッダー左**: 所属（カスタマイズ可能）
- **ヘッダー右**: 日付（自動または指定）
- **ヘッダー・フッター**: 罫線
- **フッター**: ページ番号（中央揃え）

### 見出し

自動で番号付けされます：

```typst
= 大見出し（1）
== 中見出し（1.1）
=== 小見出し（1.1.1）
```

### ヘルパー関数

#### 強調ボックス

```typst
#emphasis-box[
  重要な内容を強調表示
]
```

#### 警告ボックス

```typst
#warning-box[
  注意すべき内容
]
```

#### 枠付きボックス

```typst
#bordered-box(title: "タイトル")[
  枠で囲んだ内容
]
```

### 図表

#### 図（画像）

**実際の画像ファイルを使う場合**：

```typst
#figure(
  image("Figures/satellite.png", width: 70%),
  caption: [小型衛星のシステム構成図]
)
```

**準備手順**:
1. `Figures/` ディレクトリに画像ファイルを配置
2. 上記のコードで参照

**サンプル画像の例**（`main.typ`を参照）:
- `Figures/typst.svg` - Typstのロゴ
- `Figures/typst-github.svg` - Typst + GitHubのロゴ

**画像がない場合のプレースホルダー**：

```typst
#figure(
  rect(
    width: 60%,
    height: 150pt,
    stroke: 1pt + gray,
    fill: rgb("#f0f0f0"),
  )[
    #align(center + horizon)[
      画像プレースホルダー
    ]
  ],
  caption: [図の説明]
)
```

**複数の画像を並べる**：

```typst
#figure(
  grid(
    columns: 2,
    gutter: 1em,
    image("Figures/img1.png", width: 100%),
    image("Figures/img2.png", width: 100%),
  ),
  caption: [2つの画像を並べた例]
)
```

#### 表

```typst
#figure(
  table(
    columns: 4,
    stroke: 0.5pt,
    [項目], [値1], [値2], [値3],
    [データA], [10], [20], [30],
    [データB], [15], [25], [35],
  ),
  caption: [実験結果の比較]
)
```

### コードブロック

```typst
```python
def hello():
    print("Hello, World!")
```
\```

自動でシンタックスハイライトと背景色が適用されます。

### 数式

インライン数式: `$E = m c^2$`

ディスプレイ数式:
```typst
$
  integral_0^infinity e^(-x^2) dif x = sqrt(pi)/2
$
```

### 参考文献

本文中で引用：

```typst
先行研究 @wertz2011space によれば...
```

参考文献セクション（本文の最後に配置）：

```typst
= 参考文献 <bibliography-section>

#bibliography("references.bib", title: none, style: "ieee")
```

**重要**: 見出し番号を付けるには `= 参考文献` と `title: none` を使用してください。

## カスタマイズ可能な設定

### ページ設定（config.typ）

```typst
margin: (
  top: 3cm,      // 上マージン
  bottom: 2.5cm, // 下マージン
  left: 2cm,     // 左マージン
  right: 2cm,    // 右マージン
),
```

### フォント設定

```typst
main-font: "Noto Serif CJK JP",
main-size: 11pt,
```

### 見出しサイズ

```typst
heading-sizes: (
  level1: 18pt,
  level2: 14pt,
  level3: 12pt,
),
```

### ヘッダー・フッター設定

```typst
header-footer-config = (
  show-header: true,              // ヘッダーを表示
  header-size: 10pt,              // フォントサイズ
  header-left: none,              // 左側テキスト（noneで所属を使用）
  show-date-in-header: true,      // 日付を表示
  show-page-number: true,         // ページ番号を表示
  line-stroke: 0.5pt,             // 罫線の太さ
)
```

## よくあるカスタマイズ

### 1. マージンを変更

`config.typ`の`page-config`を編集：

```typst
margin: (
  top: 2.5cm,
  bottom: 2cm,
  left: 2.5cm,
  right: 2.5cm,
),
```

### 2. フォントサイズを変更

`config.typ`の`font-config`を編集：

```typst
main-size: 12pt,
```

### 3. 所属を変更

文書内で指定：

```typst
#show: rinko.with(
  affiliation: "あなたの研究室名 輪講資料",
  ...
)
```

### 4. 日付を指定

```typst
#show: rinko.with(
  date: (2025, 10, 19),  // 年, 月, 日
  ...
)
```

指定しない場合は自動で今日の日付が使用されます。

### 5. 画像を追加

1. `Figures/` ディレクトリに画像をコピー
2. 文書中で参照：

```bash
cp /path/to/your/image.png Figures/
```

```typst
#figure(
  image("Figures/image.png", width: 70%),
  caption: [画像の説明]
)
```

## サンプル出力

`main.typ`には以下の内容が含まれています：

- タイトルページ（タイトル、著者、所属、日付）
- ヘッダー・フッター（所属、日付、ページ番号）
- 見出しの階層例（番号付き）
- ADCSの構成要素（センサー、アクチュエータ）
- 強調ボックス、警告ボックス、枠付きボックスの例
- 実際の画像の表示例（Typstロゴ）
- 複数画像の並べ方
- プレースホルダー画像
- Pythonコードブロック
- 数式の例
- 表の例
- 参考文献（番号付き見出し）

## 新しい資料を作成する手順

### 方法1: main.typをベースにする

1. `main.typ`をコピーして新しいファイル名に変更
2. タイトル、著者、所属を編集
3. 本文を書く
4. コンパイル

```bash
cp main.typ my_seminar_2025_10_19.typ
# ファイルを編集
typst compile my_seminar_2025_10_19.typ
```

### 方法2: テンプレート全体をコピーする

このディレクトリ全体をコピーして、新しいプロジェクトのベースとして使用：

```bash
cp -r labseminar_template my_new_seminar
cd my_new_seminar
# main.typを編集
typst compile main.typ
```

## トラブルシューティング

### フォントが見つからない

システムにインストールされているフォントを確認：

```bash
typst fonts
```

`config.typ`の`main-font`を利用可能なフォントに変更してください。

### 画像が表示されない

1. 画像ファイルが`Figures/`ディレクトリに存在することを確認
2. ファイル名と拡張子が正確に一致しているか確認（大文字小文字も区別されます）
3. パスが正しいか確認（`Figures/image.png`）

### 参考文献が表示されない

1. `references.bib`が存在することを確認
2. 本文中で`@キー`（例: `@wertz2011space`）を使用していることを確認
3. `#bibliography(...)`が本文の最後にあることを確認
4. 引用されていない文献は自動的に除外されます

### ヘッダー・フッターが表示されない

1. `config.typ`で`show-header: true`と`show-page-number: true`が設定されているか確認
2. テンプレートが正しくインポートされているか確認

## 参考リンク

- [Typst公式ドキュメント](https://typst.app/docs)
- [Typst Universe](https://typst.app/universe) - パッケージとテンプレート

## ライセンス

このテンプレートは自由に使用・改変できます。
