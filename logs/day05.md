# 学習メモ

## [JavaScript Primer](https://jsprimer.net/) を利用してJavaScriptの基礎を学習しなおし中

### [オブジェクト](https://jsprimer.net/basic/object/#object)
オブジェクトはプロパティ(キーとバリューがセットになったもの)の集合
`Object`はあらゆる環境で利用できる組み込み(ビルトイン)オブジェクト

#### オブジェクトを作成する

```javascript
const obj = { // オブジェクトリテラルで作成
  "key1": "value1", // キーが文字列の場合
  key2: "value2", // キーがSymbolの場合
  key-3: "value3" // キーがSymbolの場合には変数名のルールに従わない場合NGとなる
  "key-3": "value3" // これならOK
};

obj.key1; // "value1"
obj["key1"]; // "value1"
obj.key-3; // これはNG
obj["key-3"]; // これはOK

```

```javascript
const name = "Alice";
const obj = {
  name // プロパティ名と変数名が同じ場合、省略記法で書ける
};
```

```javascript
const languages = {
  ja: "日本語",
  en: "英語"
}

const { ja, en } = languages; // [ES2015]からは分割代入でプロパティを取り出せる

// わざわざ以下のように書かなくてよくなる
const ja = languages.ja;
const en = languages.en;
```

```javascript
const obj = {};

obj.newKey = "newValue"; // ドット記法でプロパティを追加
obj["another-key"] = "another-value"; // ブラケット記法でプロパティを追加する場合は変数/変数の識別子として使えない文字列/SymbolがキーであってもOK

delete obj.newKey; // ドット記法でプロパティを削除
delete obj["another-key"]; // ブラケット記法でプロパティを削除

obj.notExistKey; // 存在しないプロパティにアクセスするとundefinedが返る
```

```javascript
const obj = { key: undefined };
if ("key" in obj) { // プロパティが存在するかどうかを調べるにはin演算子を使う
  console.log("プロパティkeyは存在する");
}

if(obj.key !== undefined) // これだとプロパティがundefinedの場合に誤判定する可能性があるので注意

Object.hasOwn(obj, "key"); // [ES2022]からはObject.hasOwnメソッドが使える
obj.hasOwnProperty("key"); // [ES2022]以降で使える

```

## 次回
[[ES2020] Optional chaining演算子（?.）](https://jsprimer.net/basic/object/#optional-chaining-operator)