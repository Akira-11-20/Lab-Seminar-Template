# 輪講資料テンプレート

研究室の輪講資料用のTypstテンプレートです。設定ファイルベースで、簡単にカスタマイズできます。

## 必要な環境

### Typstのインストール

#### 推奨: Rust（cargo）でインストール

最新版をビルドしてインストールする方法です：

```bash
# Rustがインストールされていない場合、まずRustをインストール
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh

# Typstをインストール
cargo install --git https://github.com/typst/typst --locked typst-cli
```

インストール確認：

```bash
typst --version
```

#### その他の方法

**Linux/macOS (公式インストーラ)**:

```bash
curl -fsSL https://typst.app/install.sh | sh
```

**Windows (PowerShell)**:

```powershell
irm https://typst.app/install.ps1 | iex
```

**パッケージマネージャー**:

```bash
# Homebrew (macOS/Linux)
brew install typst

# Arch Linux
pacman -S typst
```

### 推奨: VSCode拡張機能

Typstの開発には、以下のVSCode拡張機能を強く推奨します：

#### 1. Tinymist Typst (推奨)
- **拡張機能ID**: `myriad-dreamin.tinymist`
- **機能**:
  - リアルタイムプレビュー（編集しながらPDFを確認）
  - シンタックスハイライト
  - 自動補完
  - エラーチェック
  - ホバーでのドキュメント表示

**インストール方法**:
1. VSCodeを開く
2. 拡張機能ビュー (`Ctrl+Shift+X` / `Cmd+Shift+X`) を開く
3. "Tinymist Typst" を検索してインストール
4. `.typ` ファイルを開くと自動的に有効化

**使い方**:
- `.typ` ファイルを開くと、右側に自動でプレビューが表示されます
- プレビューが表示されない場合: コマンドパレット (`Ctrl+Shift+P` / `Cmd+Shift+P`) → "Typst: Show Preview"
- ファイルを編集すると、プレビューがリアルタイムで更新されます

#### 2. Typst Preview (代替)
- **拡張機能ID**: `mgt19937.typst-preview`
- Tinymistと同様のプレビュー機能を提供

**どちらを使うべきか**: Tinymistの方が新しく、機能が豊富なため推奨します。

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

## クイックスタート

### 最も簡単な方法（VSCode + 拡張機能使用）

1. **VSCodeで開く**
   ```bash
   cd labseminar_template
   code .
   ```

2. **Tinymist Typst拡張機能をインストール**（まだの場合）
   - 拡張機能ビュー (`Ctrl+Shift+X`) → "Tinymist Typst" を検索

3. **main.typを開く**
   - 自動的に右側にプレビューが表示されます
   - ファイルを編集すると、リアルタイムで更新されます

4. **編集して保存**
   - タイトル、著者名、本文を編集
   - `Ctrl+S` / `Cmd+S` で保存すると、プレビューが更新されます

5. **PDFをエクスポート**
   - プレビュー上部の「Export PDF」ボタンをクリック
   - または、コマンドパレット → "Typst: Export PDF"

### コマンドラインでの使い方

#### 1回だけコンパイル

```bash
cd labseminar_template
typst compile main.typ
```

出力ファイル名を指定：

```bash
typst compile main.typ output.pdf
```

#### 変更を監視して自動コンパイル

```bash
typst watch main.typ
```

ファイルを編集すると自動的に再コンパイルされます。`Ctrl+C` で終了。

## 使い方

### 1. 基本的な文書構造

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

### 2. 設定のカスタマイズ

[config.typ](config.typ) を編集することで、全体の設定を変更できます：
- ページマージン
- フォント設定
- 見出しサイズ
- ヘッダー・フッターの表示

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

### 方法1: main.typをベースにする（推奨）

**VSCodeを使う場合**:

1. VSCodeでこのフォルダを開く
2. [main.typ](main.typ) を右クリック → "Copy"
3. サイドバーで右クリック → "Paste" → ファイル名を変更（例: `seminar_2025_10_20.typ`）
4. 新しいファイルを開いて編集
5. Tinymist拡張機能で自動的にプレビューが表示されます

**コマンドラインを使う場合**:

```bash
cp main.typ seminar_2025_10_20.typ
# VSCodeで開く
code seminar_2025_10_20.typ
# またはコンパイル
typst compile seminar_2025_10_20.typ
```

### 方法2: テンプレート全体をコピーして新プロジェクト作成

複数の輪講資料を別々のフォルダで管理したい場合：

```bash
# テンプレート全体をコピー
cp -r labseminar_template ../seminar_2025_10_20
cd ../seminar_2025_10_20

# VSCodeで開く
code .

# main.typを編集してコンパイル
typst compile main.typ
```

### 推奨ワークフロー

1. **テンプレートフォルダ内で作業する**
   - `main.typ` をコピーして日付ごとにファイル名を変更
   - 例: `seminar_2025_10_20.typ`, `seminar_2025_10_27.typ`
   - すべての資料が同じ `Figures/` や `references.bib` を共有

2. **プロジェクトごとに分ける**
   - 大きなトピックごとにテンプレート全体をコピー
   - それぞれ独立した画像や参考文献を管理

## トラブルシューティング

### VSCode関連

#### プレビューが表示されない

**解決方法**:

1. Tinymist Typst拡張機能がインストールされているか確認
2. コマンドパレット (`Ctrl+Shift+P` / `Cmd+Shift+P`) → "Typst: Show Preview" を実行
3. VSCodeを再起動
4. 拡張機能を無効化→有効化

#### 拡張機能がエラーを出す

**解決方法**:

1. Typst CLIが正しくインストールされているか確認:
   ```bash
   typst --version
   ```

2. VSCodeの設定で正しいパスが設定されているか確認:
   - 設定 (`Ctrl+,`) → "typst" で検索
   - "Typst: Path" が正しく設定されているか確認

3. 出力パネルを確認:
   - 表示 → 出力 → "Tinymist Typst" を選択してエラーログを確認

#### 自動補完が効かない

**解決方法**:

1. `.typ` ファイルの言語モードが "Typst" になっているか確認（右下のステータスバー）
2. Tinymist拡張機能が有効になっているか確認
3. VSCodeを再起動

### Typst CLI関連

#### フォントが見つからない

システムにインストールされているフォントを確認：

```bash
typst fonts
```

[config.typ](config.typ) の `main-font` を利用可能なフォントに変更してください。

#### コンパイルエラー: "file not found"

**解決方法**:

1. カレントディレクトリが正しいか確認:
   ```bash
   pwd  # 現在のディレクトリを表示
   cd labseminar_template  # 必要に応じて移動
   ```

2. ファイル名が正しいか確認:
   ```bash
   ls *.typ  # .typファイルを一覧表示
   ```

### 画像が表示されない

**解決方法**:

1. 画像ファイルが `Figures/` ディレクトリに存在することを確認
2. ファイル名と拡張子が正確に一致しているか確認（大文字小文字も区別されます）
3. パスが正しいか確認（`Figures/image.png`）
4. 画像ファイルが破損していないか確認

### 参考文献が表示されない

**解決方法**:

1. `references.bib` が存在することを確認
2. 本文中で `@キー`（例: `@wertz2011space`）を使用していることを確認
3. `#bibliography(...)` が本文の最後にあることを確認
4. 引用されていない文献は自動的に除外されます
5. `.bib` ファイルの文法エラーがないか確認

### ヘッダー・フッターが表示されない

**解決方法**:

1. [config.typ](config.typ) で `show-header: true` と `show-page-number: true` が設定されているか確認
2. テンプレートが正しくインポートされているか確認:
   ```typst
   #import "template.typ": rinko, emphasis-box, warning-box, bordered-box
   ```
3. `#show: rinko.with(...)` が正しく記述されているか確認

## 参考リンク

### Typst公式

- [Typst公式ドキュメント](https://typst.app/docs) - 文法リファレンス
- [Typst Universe](https://typst.app/universe) - パッケージとテンプレート集
- [Typst GitHub](https://github.com/typst/typst) - ソースコード

### VSCode拡張機能

- [Tinymist Typst](https://marketplace.visualstudio.com/items?itemName=myriad-dreamin.tinymist) - 推奨拡張機能
- [Tinymist GitHub](https://github.com/Myriad-Dreamin/tinymist) - ドキュメントとissue

### 学習リソース

- [Typst Tutorial](https://typst.app/docs/tutorial/) - 公式チュートリアル
- [Typst Guide for LaTeX Users](https://typst.app/docs/guides/guide-for-latex-users/) - LaTeXからの移行ガイド
- [Typst Examples](https://github.com/typst/typst/tree/main/tests) - サンプルコード集

### コミュニティ

- [Typst Discord](https://discord.gg/2uDybryKPe) - コミュニティフォーラム
- [Typst Forum](https://forum.typst.app/) - 質問＆回答

## ライセンス

このテンプレートは自由に使用・改変できます。

---

**作成者**: あなたの名前/研究室名
**最終更新**: 2025年10月20日
