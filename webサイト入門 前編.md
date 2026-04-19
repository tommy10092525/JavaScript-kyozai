# Webサイト入門 前編

## Webの世界へようこそ！

### Webページってどうやって作られてるの？

ブラウザ（ChromeやSafariなど）でWebページを開くとき，裏では次のことが起きています。

```
あなたのPC                     サーバー
  ブラウザ  ──リクエスト──▶  Webサーバー
           ◀──HTMLファイルなど──
```

1. ブラウザが「このページを見せて」とサーバーに**リクエスト**を送る
2. サーバーが**HTMLファイル**などを返す
3. ブラウザがファイルを読み込んで画面に表示する

つまり，Webページとは「ブラウザが読み込んで表示するファイル」です。そのファイルを作れるようになるのがこの教材のゴールです。

---

### Webサイトの構成要素

Webサイトは主に3つの言語で作られています。

| 言語 | 役割 | たとえると… |
|---|---|---|
| **HTML** | ページの構造・内容 | 骨格 |
| **CSS** | 見た目・デザイン | 服・化粧 |
| **JavaScript** | 動き・インタラクション | 筋肉 |

この教材の前編では **HTML** と **CSS** を学びます。

---

### 環境構築

コードを書くためのエディタをインストールします。ここでは **Visual Studio Code（VS Code）** を使います。

1. [https://code.visualstudio.com/](https://code.visualstudio.com/) からダウンロードしてインストールする
2. インストールできたら VS Code を起動する
3. 適当なフォルダ（例：`my-website`）を作り，VS Code で開く

ファイルを開くには「ファイル → フォルダを開く」からフォルダを選択します。

---

## 第1章 実際にHTMLを書いてみよう

### サンドイッチのルール

HTMLは**タグ**と呼ばれる記号で文章を囲むことで，「ここは見出しです」「ここは段落です」という意味を伝えます。

タグには**開始タグ**と**終了タグ**があり，内容をサンドイッチのように挟みます。

```
<タグ名>内容</タグ名>
  ↑開始タグ   ↑終了タグ（スラッシュがつく）
```

例：
```html
<h1>大きな見出し</h1>
<p>本文のテキスト</p>
```

終了タグを書き忘れると表示が崩れるので注意しましょう。

---

### HTMLファイルの作成

VS Code で `index.html` という名前のファイルを作りましょう。

1. VS Code の左側のファイルツリーで右クリック → 「新しいファイル」
2. ファイル名を `index.html` と入力して Enter

ファイルが作成されたら，次のように入力してみましょう。

```html
こんにちは！
```

ファイルを保存（Ctrl+S / Cmd+S）してブラウザで開くと，「こんにちは！」と表示されます。

---

### h1 見出しタグ

`<h1>` タグは一番大きな見出しを表します。h は "heading"（見出し）の頭文字です。

```html
<h1>私のWebサイト</h1>
```

`<h1>` から `<h6>` まであり，数字が大きくなるほど見出しが小さくなります。

```html
<h1>一番大きな見出し</h1>
<h2>二番目の見出し</h2>
<h3>三番目の見出し</h3>
```

---

### p 段落タグ

`<p>` タグは段落（本文）を表します。p は "paragraph"（段落）の頭文字です。

```html
<p>これは最初の段落です。文章がここに入ります。</p>
<p>これは二番目の段落です。段落ごとに改行されます。</p>
```

`<p>` タグで囲むと，段落と段落の間に自動的に余白が入ります。

---

### li リストタグ①

`<li>` タグはリストの各項目を表します。li は "list item"（リスト項目）の頭文字です。

```html
<li>りんご</li>
<li>みかん</li>
<li>ぶどう</li>
```

ただし，`<li>` 単体では正しいリストになりません。次で紹介する `<ul>` または `<ol>` と組み合わせて使います。

---

### ul, ol リストタグ②

`<ul>` は**順序なし**リスト（箇条書き），`<ol>` は**順序あり**リスト（番号付き）です。

#### ul（Unordered List）- 箇条書き

```html
<ul>
  <li>りんご</li>
  <li>みかん</li>
  <li>ぶどう</li>
</ul>
```

表示：
- りんご
- みかん
- ぶどう

#### ol（Ordered List）- 番号付き

```html
<ol>
  <li>材料を用意する</li>
  <li>水を沸騰させる</li>
  <li>麺を入れる</li>
</ol>
```

表示：
1. 材料を用意する
2. 水を沸騰させる
3. 麺を入れる

---

### img 画像タグ

`<img>` タグは画像を表示します。img は "image" の略です。

```html
<img src="cat.jpg" alt="猫の写真">
```

`<img>` タグは**終了タグがありません**（自己完結型タグ）。

| 属性 | 意味 | 必須 |
|---|---|---|
| `src` | 画像ファイルのパス（場所） | 必須 |
| `alt` | 画像が表示できないときの代替テキスト | 推奨 |
| `width` | 表示する幅（ピクセル） | 任意 |
| `height` | 表示する高さ（ピクセル） | 任意 |

```html
<img src="photo.jpg" alt="風景写真" width="400">
```

---

### a リンクタグ

`<a>` タグはリンクを作ります。a は "anchor"（錨）の頭文字です。

```html
<a href="https://google.com">Googleへ移動</a>
```

`href` 属性にリンク先のURLを指定します。

#### 別ページへのリンク（外部リンク）

```html
<a href="https://example.com" target="_blank">外部サイト（新しいタブで開く）</a>
```

`target="_blank"` を付けると新しいタブで開きます。

#### 同じサイト内のページへのリンク（内部リンク）

```html
<a href="about.html">自己紹介ページへ</a>
```

---

### html, head, body タグ

実際のHTMLファイルには，ページの骨格となる決まった構造があります。

```html
<!DOCTYPE html>
<html lang="ja">
  <head>
    <meta charset="UTF-8">
    <title>ページのタイトル</title>
  </head>
  <body>
    <h1>こんにちは！</h1>
    <p>ここに本文を書きます。</p>
  </body>
</html>
```

| タグ・宣言 | 役割 |
|---|---|
| `<!DOCTYPE html>` | このファイルがHTMLであることをブラウザに伝える |
| `<html>` | HTMLファイル全体を囲む |
| `lang="ja"` | ページの言語を日本語に設定する属性 |
| `<head>` | ブラウザへの設定情報（画面には表示されない） |
| `<meta charset="UTF-8">` | 日本語などが文字化けしないようにする設定 |
| `<title>` | ブラウザのタブに表示されるタイトル |
| `<body>` | 画面に表示される内容をここに書く |

これからHTMLを書くときは，この構造を土台として使いましょう。

---

### 演習：自己紹介ページを作ろう

上で学んだタグを使って，自己紹介ページを作ってみましょう。

**完成イメージ**
```
# 自己紹介

私の名前は○○です。

好きなもの
 ・ラーメン
 ・プログラミング
 ・音楽

[GitHubを見る]
```

#### index.html

```html
<!DOCTYPE html>
<html lang="ja">
  <head>
    <meta charset="UTF-8">
    <title>自己紹介</title>
  </head>
  <body>
    <h1>自己紹介</h1>
    <p>私の名前は○○です。</p>

    <h2>好きなもの</h2>
    <ul>
      <li>ラーメン</li>
      <li>プログラミング</li>
      <li>音楽</li>
    </ul>

    <a href="https://github.com">GitHubを見る</a>
  </body>
</html>
```

---

## 第2章 CSSでスタイリングしよう

### CSSってなんだ？

HTML だけでは文字が並んでいるだけのシンプルなページになります。CSS を使うと，文字の色やサイズ，背景色などを自由に変えられます。

CSS は **Cascading Style Sheets** の略です。「スタイルの設定書」のようなイメージです。

---

### CSSを体験してみよう！

まず `style.css` というファイルを作成し，HTML から読み込みます。

#### style.css を作成する

VS Code で `style.css` という新しいファイルを作り，次のように入力してみましょう。

```css
h1 {
  color: red;
}
```

#### HTML から CSS を読み込む

`<head>` の中に `<link>` タグを追加します。

```html
<head>
  <meta charset="UTF-8">
  <title>自己紹介</title>
  <link rel="stylesheet" href="style.css">
</head>
```

ブラウザで開くと，h1 の文字が赤くなります。

---

### CSSの文法

CSS の基本的な書き方は次の通りです。

```css
セレクタ {
  プロパティ: 値;
  プロパティ: 値;
}
```

```css
h1 {
  color: blue;
  font-size: 32px;
}
```

| 用語 | 意味 | 例 |
|---|---|---|
| **セレクタ** | どの要素に適用するかの指定 | `h1`，`p`，`.title` |
| **プロパティ** | 変えたいスタイルの種類 | `color`，`font-size` |
| **値** | プロパティに設定する内容 | `red`，`32px` |

`;`（セミコロン）を忘れるとその行以降のスタイルが反映されなくなるので注意しましょう。

---

### color 文字の色を変える

`color` プロパティで文字の色を変えられます。

```css
h1 {
  color: red;
}

p {
  color: #333333;
}
```

色の指定方法は主に3種類あります。

| 指定方法 | 例 | 特徴 |
|---|---|---|
| 色名 | `red`，`blue`，`green` | 覚えやすいが種類が限られる |
| HEX（16進数） | `#ff0000`，`#333` | よく使われる。色の細かい指定ができる |
| RGB | `rgb(255, 0, 0)` | 赤・緑・青の強さで指定する |

```css
h1 { color: tomato; }          /* 色名 */
p  { color: #3d3d3d; }         /* HEX */
a  { color: rgb(0, 100, 200); }/* RGB */
```

---

### font-size 文字の大きさを変える

`font-size` プロパティで文字のサイズを変えられます。

```css
h1 {
  font-size: 48px;
}

p {
  font-size: 16px;
}
```

単位は主に `px`（ピクセル）を使います。ブラウザの標準的な文字サイズは `16px` です。

```css
/* よく使うサイズの目安 */
h1 { font-size: 32px; }
h2 { font-size: 24px; }
p  { font-size: 16px; }
small { font-size: 12px; }
```

---

### font-family 文字の種類（フォント）を変える

`font-family` プロパティでフォントを変えられます。

```css
body {
  font-family: "Helvetica Neue", Arial, sans-serif;
}
```

複数のフォントをカンマで区切って並べると，先頭から順に使用可能なフォントが適用されます（フォールバック）。

```css
/* ゴシック体 */
p {
  font-family: "Hiragino Sans", "Meiryo", sans-serif;
}

/* 明朝体 */
h1 {
  font-family: "Hiragino Mincho ProN", "MS Mincho", serif;
}
```

---

### width, height 幅・高さを変える

`width` と `height` プロパティで要素の大きさを指定できます。

```css
img {
  width: 300px;
  height: 200px;
}
```

`%`（パーセント）を使うと，親要素に対する割合で指定できます。

```css
img {
  width: 100%;  /* 親要素の幅いっぱいに広げる */
}

.container {
  width: 80%;   /* 画面幅の80% */
  height: 200px;
}
```

---

### background-color 背景に色を付ける

`background-color` プロパティで背景色を設定できます。

```css
body {
  background-color: #f0f0f0;
}

h1 {
  background-color: yellow;
}
```

ページ全体の背景色を変えたいときは `body` に指定します。

```css
body {
  background-color: #1a1a2e; /* 濃い紺色 */
  color: white;               /* 文字色を白に */
}
```

---

### 特定の場所にだけデザインを当てる

タグ名でセレクタを指定すると，そのタグ**すべて**にスタイルが適用されます。特定の要素だけにスタイルを当てたいときは `class` や `id` を使います。

#### class

`class` は**複数の要素**に同じスタイルを当てたいときに使います。

HTML に `class="クラス名"` を付けます。

```html
<p class="highlight">この段落だけ強調されます。</p>
<p>この段落は普通のスタイルです。</p>
<p class="highlight">こちらも強調されます。</p>
```

CSS では `.クラス名` と書いてセレクタを指定します（`.` を先頭に付ける）。

```css
.highlight {
  color: red;
  font-size: 20px;
}
```

#### id

`id` は**ページ内で1つだけ**の要素に固有のスタイルを当てたいときに使います。

HTML に `id="ID名"` を付けます。

```html
<h1 id="main-title">メインタイトル</h1>
<p>本文テキスト。</p>
```

CSS では `#ID名` と書いてセレクタを指定します（`#` を先頭に付ける）。

```css
#main-title {
  color: navy;
  font-size: 40px;
  text-align: center;
}
```

#### class と id の使い分け

| | class | id |
|---|---|---|
| HTML での書き方 | `class="名前"` | `id="名前"` |
| CSSでのセレクタ | `.名前` | `#名前` |
| 同じページで使える数 | 何度でも | 1回だけ |
| 用途 | 同じスタイルを複数箇所に | 1つの要素に固有のスタイルを |

---

### 演習：自己紹介ページをスタイリングしよう

第1章で作った自己紹介ページに CSS でデザインを追加しましょう。

**完成イメージ**
- 背景色をグレー系にする
- h1 を大きく・中央揃えにする
- 特定の段落の文字色を変える
- リンクのデザインを変える

#### style.css

まずは自分で書いてみましょう。以下のステップを参考にしてください。

1. `body` に `background-color` で背景色を付ける
2. `h1` に `font-size`・`color`・`text-align: center` を設定する
3. 自己紹介文の `<p>` タグに `class="intro"` を付け，CSS でスタイルを当てる
4. `<a>` タグにスタイルを当てる

---

<details>
<summary>解答例を見る</summary>

#### index.html（変更箇所）

```html
<body>
  <h1>自己紹介</h1>
  <p class="intro">私の名前は○○です。</p>

  <h2>好きなもの</h2>
  <ul>
    <li>ラーメン</li>
    <li>プログラミング</li>
    <li>音楽</li>
  </ul>

  <a href="https://github.com">GitHubを見る</a>
</body>
```

#### style.css

```css
body {
  background-color: #f5f5f5;
  font-family: "Hiragino Sans", Arial, sans-serif;
}

h1 {
  font-size: 40px;
  color: #333333;
  text-align: center;
}

h2 {
  font-size: 24px;
  color: #555555;
}

.intro {
  color: #666666;
  font-size: 18px;
}

a {
  color: #0077cc;
}
```

</details>

---

**発展課題**（余裕があれば挑戦してみよう）

- `border` プロパティで要素に枠線を付ける（例：`border: 1px solid black;`）
- `padding` プロパティで要素の内側に余白を付ける
- `margin` プロパティで要素の外側に余白を付ける
- `text-align: center` でテキストを中央揃えにする
