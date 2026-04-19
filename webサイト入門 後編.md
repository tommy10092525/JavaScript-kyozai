# Webサイト入門 後編

## 第4章 プログラミングでWebサイトに動きをつけよう

### DOMとは（HTMLとJavaScriptのつながり）

ブラウザはHTMLファイルを読み込むとき，タグの入れ子構造を「**DOMツリー**」と呼ばれるデータ構造に変換します。

```
<body>
  <h1 id="title">Hello</h1>
  <p>テキスト</p>
</body>
```

```
body
├── h1#title  "Hello"
└── p         "テキスト"
```

JavaScriptはこのDOMツリーにアクセスして，要素の内容や見た目を**後から書き換える**ことができます。これが「Webサイトに動きをつける」仕組みです。

JavaScriptをHTMLに読み込むには，`<script>`タグを使います。`</body>`の直前に書くのが一般的です。

```html
<!DOCTYPE html>
<html>
  <head>
    <title>サンプル</title>
  </head>
  <body>
    <h1 id="title">Hello</h1>

    <script src="script.js"></script>
  </body>
</html>
```

---

### querySelector で要素を取得する

`document.querySelector()` を使うと，HTMLの要素をJavaScriptから取得できます。引数にはCSSと同じセレクタを文字列で渡します。

```javascript
// タグ名で取得
const heading = document.querySelector("h1");

// クラス名で取得（先頭に . をつける）
const box = document.querySelector(".container");

// IDで取得（先頭に # をつける）
const title = document.querySelector("#title");
```

複数の要素が一致する場合，**最初の1つだけ**が返されます。  
要素が見つからない場合は `null` が返ります。

---

### textContent/innerHTML で内容を書き換える

取得した要素の内容を書き換えるには `.textContent` または `.innerHTML` を使います。

#### textContent
テキストだけを書き換えます。HTMLタグは文字列として扱われるため，安全に使えます。

```javascript
const title = document.querySelector("#title");
title.textContent = "こんにちは！";
```

#### innerHTML
HTML込みで書き換えます。タグも反映されます。

```javascript
const box = document.querySelector(".container");
box.innerHTML = "<strong>太字のテキスト</strong>";
```

ユーザーが入力した文字列をそのまま `innerHTML` に渡すと，悪意のあるスクリプトが実行されてしまう危険性があります。ユーザー入力を表示するときは必ず `textContent` を使ってください。

---

### style で見た目を変える

取得した要素の `.style` プロパティを使うと，CSSを直接書き換えられます。

```javascript
const title = document.querySelector("#title");

title.style.color = "red";
title.style.fontSize = "32px";
title.style.backgroundColor = "yellow";
```

CSSのプロパティ名はハイフン区切り（`font-size`）ですが，JavaScriptでは**キャメルケース**（`fontSize`）で書きます。

| CSS | JavaScript |
|---|---|
| `color` | `style.color` |
| `font-size` | `style.fontSize` |
| `background-color` | `style.backgroundColor` |
| `display` | `style.display` |

---

### 関数（function）の基礎

**関数**とは，処理をまとめて名前をつけたものです。同じ処理を何度も書かずに済み，後で出てくる `addEventListener` にも必要です。

#### function キーワードによる定義

```javascript
function greet() {
  console.log("こんにちは！");
}

greet(); // "こんにちは！" と出力される
```

#### 引数（ひきすう）
関数を呼び出すときに値を渡せます。

```javascript
function greet(name) {
  console.log("こんにちは，" + name + "さん！");
}

greet("Tommy"); // "こんにちは，Tommyさん！"
greet("Alice"); // "こんにちは，Aliceさん！"
```

#### 戻り値
`return` を使うと，関数の結果を呼び出し元に返せます。

```javascript
function add(a, b) {
  return a + b;
}

const result = add(3, 5);
console.log(result); // 8
```

#### アロー関数
`function` キーワードを使わない，短い書き方です。動作は同じです。

```javascript
const greet = (name) => {
  console.log("こんにちは，" + name + "さん！");
};

const add = (a, b) => {
  return a + b;
};
```

---

### addEventListener でイベントを検知する

`addEventListener` を使うと，「ボタンがクリックされた」「キーが押された」などの**イベント**が起きたときに処理を実行できます。

```javascript
要素.addEventListener("イベント名", 実行する関数);
```

#### クリックイベント

```html
<!-- HTML -->
<button id="btn">クリック！</button>
<p id="message">ここに表示されます</p>
```

```javascript
// JavaScript
const button = document.querySelector("#btn");
const message = document.querySelector("#message");

button.addEventListener("click", () => {
  message.textContent = "ボタンがクリックされました！";
});
```

`"click"` の部分をイベント名と呼びます。よく使うイベント名を以下に示します。

| イベント名 | タイミング |
|---|---|
| `"click"` | クリックされたとき |
| `"change"` | 入力内容が変わったとき |
| `"keydown"` | キーが押されたとき |

---

### input要素から値を取得する

`<input>` 要素に入力された文字列は，`.value` プロパティで取得できます。

```html
<!-- HTML -->
<input type="text" id="nameInput" placeholder="名前を入力">
<button id="btn">送信</button>
<p id="result"></p>
```

```javascript
// JavaScript
const button = document.querySelector("#btn");

button.addEventListener("click", () => {
  const input = document.querySelector("#nameInput");
  const name = input.value;
  console.log(name); // 入力された文字列が出力される
});
```

`.value` は読み取るだけでなく，書き込みもできます。

```javascript
input.value = ""; // 入力欄を空にする
```

---

### 演習：名前入力フォームを作ろう

テキストボックスに名前を入力してボタンを押すと，「こんにちは，○○さん！」と表示されるページを作ってみましょう。

**完成イメージ**
```
[ Tommy      ] [送信]

こんにちは，Tommyさん！
```

#### HTMLファイル（index.html）

```html
<!DOCTYPE html>
<html lang="ja">
  <head>
    <meta charset="UTF-8">
    <title>名前入力フォーム</title>
  </head>
  <body>
    <input type="text" id="nameInput" placeholder="名前を入力してください">
    <button id="btn">送信</button>
    <p id="result"></p>

    <script src="script.js"></script>
  </body>
</html>
```

#### JavaScriptファイル（script.js）

まずは自分で書いてみましょう。以下のステップを参考にしてください。

1. `querySelector` で `#btn`，`#nameInput`，`#result` の3つの要素を取得する
2. `#btn` に `"click"` イベントを登録する
3. クリックされたら `#nameInput` の `.value` を取得する
4. 取得した値を使って `#result` の `.textContent` を書き換える
5. 名前が空のときは「名前を入力してください」と表示する（if文を使う）

---

<details>
<summary>解答を見る</summary>

```javascript
const button = document.querySelector("#btn");
const nameInput = document.querySelector("#nameInput");
const result = document.querySelector("#result");

button.addEventListener("click", () => {
  const name = nameInput.value;

  if (name === "") {
    result.textContent = "名前を入力してください";
  } else {
    result.textContent = "こんにちは，" + name + "さん！";
  }
});
```

</details>

---

**発展課題**（余裕があれば挑戦してみよう）

- 送信後に入力欄を空にする（`nameInput.value = ""`）
- 表示した文字の色を `style.color` で変える
- 「リセット」ボタンを追加して，メッセージを消せるようにする
