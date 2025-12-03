# 学習メモ

## [JavaScript Primer](https://jsprimer.net/) を利用してJavaScriptの基礎を学習しなおし中

### [文と式](https://jsprimer.net/basic/statement-expression/#statement-and-expression)

#### 式
値を生成し、変数に代入できるもの。リテラルや変数、関数呼び出し、式と演算子の組み合わせなど。
評価した結果を変数に代入できるのならばそれは式という理解でOKっぽい。

```javascript
const fn = function() { // これは関数式。変数に代入できている。
  return 1; // これも式
};

#### 文
if文やfor文などの処理するひとつひとつの単位。
JSだとセミコロンを置くことで文の区切りを表現する。

例えばif文は式ではないので変数に代入することはできない。

```javascript
const x = if (true) { // これは文なので変数に代入できない
  console.log("Hello");
}
```

#### 式文
式は文になることができる。文になった式のことを式文と呼ぶ。
式文は文の一種なのでセミコロンで区切る。

#### ブロック文
文をまとめるための文。`{}`で囲む。
```javascript
{
  console.log("Hello");
  console.log("World");
}
```

if文やfor文はブロック文と組み合わせて複数の文をまとめて処理することが多い
```javascript
if (true) {
  console.log("Hello");
  console.log("World");
} // ブロックで終わるときにはセミコロン不要

if (true) console.log("Hello"); // ブロック文を使わずに1つの文だけ処理することもできるがセミコロンいる
```

```javascript
{
  const x = 1;
}
// ブロックの外なのでxは参照できない
{
  const x = 2; // ブロックごとにスコープ別れているので再定義OK。REPLとかだと便利らしい。
}
```

#### 関数宣言と関数式

```javascript
function learn() {
} // 文なのでセミコロン不要
const fn = function() {
}; // 式なのでセミコロン必要
```

### [条件分岐](https://jsprimer.net/basic/condition/#conditional-branch)

#### if文
```javascript
if (条件式) {
  // 条件式がtrueのときに実行される文
} else if (別の条件式) {
  // 別の条件式がtrueのときに実行される文
} else {
  // どの条件式もtrueでなかったときに実行される文
}
```

```javascript
if true
  console.log("Hello"); // 実行する文が1つだけならブロック省略OK
```

条件式にboolean型以外の値を指定した場合は暗黙的な型変換が行われる。
falsyな値は覚えてしまったほうがいい
- `false`
- `undefined`
- `null`
- `0`
- `0n`（BigIntの0）
- `""`（空文字列）
- `NaN`

#### switch文
```javascript
switch (式) {
  case 値1:
    // 式の評価結果が値1と厳密に等しい(つまり===)場合に実行される文
    break; // breakがないと次のcaseも実行されてしまう
  case 値2:
    // 式の評価結果が値2と厳密に等しい場合に実行される文
    break;
  default:
    // どのcaseにも該当しなかった場合に実行される文
    break;
}
```

### [ループと反復処理](https://jsprimer.net/basic/loop/#loop-and-iteration)

#### while文
```javascript
while (条件式) { // 条件式が常にtrueの場合は無限ループになるので注意
  // 条件式がtrueの間繰り返し実行される文
}
```

#### do-while文
```javascript
do {
  // 最低1回は実行される文
} while (条件式); // 条件式がtrueの間繰り返し実行される
```

#### for文
```javascript
for (初期化式; 条件式; 増分式) {
  // 条件式がtrueの間繰り返し実行される文
}
```

#### 配列のforEachメソッド
```javascript
const array = [1, 2, 3];
array.forEach(currentValue => { // 無名関数を引数に渡している
  // 配列の各要素に対して繰り返し実行される文
});
```

#### for...in文
```javascript
for (プロパティ名 in オブジェクト) {
  // オブジェクトのすべての列挙可能なプロパティに対して繰り返し実行される文
}
```

```javascript
const obj = { a: 1, b: 2, c: 3 };
for (const key in obj) {
  console.log(key); // a, b, c
  console.log(obj[key]); // 1, 2, 3
}

Object.keys(obj).forEach(key => {
  console.log(key); // a, b, c
  console.log(obj[key]); // 1, 2, 3
}); // こっちのほうが安全らしい。for...inだと継承元のプロパティも列挙されるといった意図しない挙動になることがある
```

#### for...of文
`Symbol.iterator`という特別な名前のメソッドを持つオブジェクト（イテラブルオブジェクト）を反復処理するための文。

```javascript
for (変数名 of イテラブルオブジェクト) {
  // イテラブルオブジェクトの各要素に対して繰り返し実行される文
}
```

```javascript
const array = [10, 20, 30];
for (const value of array) {
  console.log(value); // 10, 20, 30
}

for (const value in array) {
  console.log(value); // 0, 1, 2 （for...inだと配列のインデックスが出力されるので注意）
}
```

## 次回
[オブジェクト](https://jsprimer.net/basic/object/#object)
