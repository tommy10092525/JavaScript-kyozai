# JavaScript応用  
## 目次
- Progateからの追加構文
- 配列メソッド
- 非同期処理
- Viteを使ったReactの導入
- React入門
- React基礎
## はじめに
この教材ではReactを用いて簡単なフロントエンドが作成できることを目標としています。  
Progate相当のJavaScriptが身についていることを前提としているため，まだできていない方はそちらを先に身に着けてください
## Progateからの追加構文
### 分割代入（オブジェクト）
  オブジェクトのプロパティを変数として取り出したいときには`let(const){プロパティ名…}=取りしたいオブジェクト`と書けます。  
```javascript
const getUser=()=>{
  return {id:1,name:"tommy"}
}

const user=getUser();
const {id,name}=user
// const id=user.id,name=user.name
```
上ではuserオブジェクトから`id`プロパティと`name`プロパティを取り出しています。

### 分割代入（配列）
```javascript
const numbers=[3,1,4,1,5,9,2,6,5]
const [first,second,third]=numbers
// const first=numbers[0],second=numbers[1],third=numbers[2];
```
配列の要素を変数として取り出したいときには`let(const) [変数名…]=取り出したい配列`と書けます。右では`numbers`配列から1~3番目の要素を`first`から`third`に取り出しています。

### 【前提】 immutableについて
すべての変数（インスタンス）はimmutableかどうかが設定されています。
immutableなオブジェクトとは作成後にその状態を変えることのできないオブジェクトです。
例えば`let n=1`，`const name="tommy"`など数値型，文字列型，真偽型，などは作成した後に変えることができません。
```javascript
let n=1
n++

let name="tommy"
name[0]="s"

let numbers=[]
numbers.push(2)
console.log(n,name,numbers)
// 2 tommy numbers
```
- この場合`n`の値は1から2に変化していますが，内部的には「1」という数値は一度破棄され，「2」という新しい実態が生成されています。
- `name`はimmutableなのでインデックスで文字を参照することはできますが，文字を変更することはできません。
- 対して，配列`numbers`はimmutable(不変)なので`.push(1)`を行った後も同じ実態が維持されています。
immutableな値は明示的にnewしない限り新しく作り直されることはありません。
```javascript
let numbers=[]
let newNumbers=numbers
numbers.push(1)
console.log(newNumbers)
// [1]
// 
```
`numbers`と`newNumbers`は同じ実態を参照しているので，`numbers`に行った変更が`newNumbers`でも反映されています。
`[]`は`new Array()`，`{}`は`new Object()`の特別な書き方です。それぞれ`Array`と`Object`というクラスをインスタンス化しています。

### スプレッド構文
#### iterableオブジェクト
```javascript
// React useStateの例
// todosは配列
setTodos(prev=>{
  const newTodos=[getNewTodo(),...todos];
  return newTodos;
})
```
iterableオブジェクト(≒配列)の要素を1つずつ取り出したい場合に`…変数`と表記します。  
`...変数`は`変数[0],変数[1],変数[2]`…と同じです。  
配列でないものを明示的に配列でないものを配列にしたい場合や，配列からimmutableに新し配列を生成したい場合に用います。
#### スプレッド構文があると便利な例
```javascript
const URLs=[...document.querySelectorAll("a")].map(a=>{
  return a.href
})
```
この場合`document.querySelectorAll`の返り値は`NodeList<HTMLAnchorElement>`であり配列ではありません。よってそのままでは`map`が使えませんのでスプレッド構文で配列に変換してから`map`を実行しています。

#### スプレッド構文（オブジェクト）
```javascript
const todo={content:"勉強する",createdAt:new Date()}
const newTodo={id:crypto.randomUUID(),...todo}
```
オブジェクトのプロパティを列挙したい場合にに使います。上の例では`{id:crypto.randomUUID(),...todo}`は`{id:crypto.randomUUID(),content:todo.content,createdAt:todo.createdAt}`と同じです。

### 配列メソッド

