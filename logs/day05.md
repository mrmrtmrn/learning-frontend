# 学習メモ

## [JavaScript Primer](https://jsprimer.net/) を利用してJavaScriptの基礎を学習しなおし中

### [オブジェクト](https://jsprimer.net/basic/object/#object)
オブジェクトはプロパティ(キーとバリューがセットになったもの)の集合
`Object`はあらゆる環境で利用できる組み込み(ビルトイン)オブジェクト

#### オブジェクト

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

```javascript
  // ネストしたプロパティにアクセスする場合、途中のプロパティがundefinedだとエラーになるので上位のプロパティが存在するかどうかを確認する必要がある
if ( obj.propertySet !== undefined && obj.propertySet.property !== undefined ) {
  console.log(obj.propertySet.property);
} else {
  console.log("プロパティが存在しない");
}

// Optional Chaining(オプショナルチェイニング)演算子[ES2020]を使うと簡潔に書ける
// プロパティがあればその値を返し、なければundefinedを返す。undefinedの場合はNullish coalescingによって右辺の値が返る
console.log( obj.propertySet?.property ?? "プロパティが存在しない" );

// ブラケット記法でも使える
console.log( obj["propertySet"]?.["property"] ?? "プロパティが存在しない" );

```

```javascript
const obj = { key: "value" };
console.log(String(obj)); // "[object Object]" Stringコンストラクタは引数に渡されたオブジェクトのtoStringメソッドを呼び出す

const customObj = {
  key: "value",
  toString() { // オブジェクトにtoStringメソッドを定義するとStringコンストラクタで呼び出されたときにそのメソッドが実行される
    return `customObj: { key: ${this.key} }`;
  }
}

console.log(String(customObj)); // "customObj: { key: value }"
```

#### Objectクラスの持つ主な静的メソッド
```javascript
const obj = { a: 1, b: 2, c: 3 };
Object.keys(obj); // ["a", "b", "c"] オブジェクトのすべての列挙可能なプロパティ名を配列で返す
Object.values(obj); // [1, 2, 3] オブジェクトのすべての列挙可能なプロパティの値を配列で返す
Object.entries(obj); // [["a", 1], ["b", 2], ["c", 3]] オブジェクトのすべての列挙可能なプロパティのキーと値のペアを配列で返す
```

```javascript
const obj1 = { a: 1 };
const obj2 = { b: 2 };

// [ES2015] Object.assign(target, ...sources)
const mergedObj = Object.assign({}, obj1, obj2); // { a: 1, b: 2 } 複数のオブジェクトを結合して新しいオブジェクトを作成する。第1引数には空のオブジェクトでなくてもよいが、元のオブジェクトが変更されるので要注意
```
```javascript
const obj1 = { a: 1 };
const obj2 = { b: 2 };

// [ES2018] スプレッド構文
// オブジェクトリテラルの中で...を使うとオブジェクトを展開できる
// オブジェクトリテラルの中でしか使えないので必ず新しいオブジェクトを返す
const mergedObj = { ...obj1, ...obj2 }; // { a: 1 , b: 2 }
```

```javascript
// オブジェクトの浅いコピーを作成する。objの直下のプロパティのみコピーされる
// 深いコピーをする場合には再帰的に浅いコピーをする [参考実装](https://jsprimer.net/basic/object/#copy)
Object.assing({}, obj);
```

## 次回

[プロトタイプオブジェクト](https://jsprimer.net/basic/prototype-object/#prototype-object)