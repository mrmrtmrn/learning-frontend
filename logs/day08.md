# 学習メモ

## [JavaScript Primer](https://jsprimer.net/) を利用してJavaScriptの基礎を学習しなおし中

### [文字列](https://jsprimer.net/basic/string/)

文字列リテラルには3種類
- シングルクォート(')
- ダブルクォート(")
  - シングルクォートとダブルクォートは同じ意味合い
- バッククォート(`)
  - ES2015から導入された。テンプレートリテラルと呼ばれる。

バッククォートのシングルクォート/ダブルクォートとの違いは文字列中に改行を入れ込めること。
```javascript
const multiline = `これは
複数行の
文字列です。`;
console.log(multiline);
// これは
// 複数行の
// 文字列です。

// エスケープシーケンスでの表現を使えばダブルクォートでも改行を表現できる
const multiline2 = "これは\n複数行の\n文字列です。";
console.log(multiline2);
// これは
// 複数行の
// 文字列です。

// どの文字列リテラルでもそのリテラルを表現したい場合にはエスケープする必要がある
const singleQuote = 'It\'s a pen.'; // シングルクォート
const doubleQuote = "He said, \"Hello.\""; // ダブルクォート
const backQuote = `This is a backtick: \``; // バッククォート


// 文字列結合したいときは以下のパターンがある
const str1 = "Hello, " + "world!"; // プラス演算子
const name = "Alice";
const str2 = `Hello, ${name}!`; // テンプレートリテラルを使う場合
console.log(str1); // "Hello, world!"
console.log(str2); // "Hello, Alice!"
```

```javascript
// 配列のようにインデックスで各文字にアクセスできる
const str = "JavaScript";
console.log(str[0]); // "J"
console.log(str[4]); // "S"
console.log(str[99]); // undefined 存在しないインデックスにアクセスするとundefinedが返る
```

```javascript
// 正規表現には以下のふたつの表現がある

// スラッシュで囲むパターン。評価されるタイミングがソースコードを解釈(ロード)する時なのでロードした時点で構文エラーになる場合がある。コードを書いた時点でパターンが決まっているパターンで使う
const regex1 = /ab+c/;

// RegExpコンストラクタで生成するパターン。評価されるタイミングが実行時なので動的にパターンを生成したい場合に使う(/\d{count}/ のように変数を使いたいときとか)
const regex2 = new RegExp("ab+c");
```

[文字列とUnicode](https://jsprimer.net/basic/string-unicode/)はスキップ

## 参考
URLやファイルパスといった典型的なものは専用の仕組みが用意されているので使うようにしよう
- [URL](https://developer.mozilla.org/ja/docs/Web/API/URL)
- [Path](https://nodejs.org/api/path.html)

## 次回
- [ラッパーオブジェクト](https://jsprimer.net/basic/wrapper-object/)
