# 学習メモ

## [JavaScript Primer](https://jsprimer.net/) を利用してJavaScriptの基礎を学習しなおし中

### [プロトタイプオブジェクト](https://jsprimer.net/basic/prototype-object/#prototype-object)


`console.log(typeof Object.prototype.toString); // "function"`のように,`prototype`オブジェクトに組み込まれているメソッドのことをプロトタイプメソッドと呼ぶ。

Objectのインスタンスは`Object.prototype`に定義されたプロトタイプメソッドを継承しているため,すべてのオブジェクトで利用できる。

```javascript
const obj = { a: 1, b: 2 };

// 同じtoStringメソッドを参照している
console.log(obj.toString === Object.prototype.toString); // true
```

```javascript
const obj = {
  toString() {
    return "custom toString method";
  }
}

console.log(obj.toString === Object.prototype.toString); // false オブジェクトにtoStringメソッドを定義するとプロトタイプメソッドは上書きされるため参照が変わる。
```

```javascript
const obj = {};

console.log(Object.hasOwn(obj, "toString")); // false プロトタイプメソッドはオブジェクトの直下には存在しないためfalseが返る
console.log("toString" in obj); // true in演算子はプロトタイプチェーン上に存在するプロパティも検出するためtrueが返る
```

```javascript
const array = [1, 2, 3];

console.log(array.hasOwnProperty === Object.prototype.hasOwnProperty); // true 配列もオブジェクトの一種なのでObject.prototypeのプロトタイプメソッドを継承している

console.log(array.toString()); // "1,2,3" 配列に対してtoStringメソッドを呼び出すと配列の要素をカンマ区切りで連結した文字列が返る。配列はArray.prototypeに独自のtoStringメソッドが定義されているためObject.prototypeのtoStringメソッドは上書きされる
```

```javascript
const noParentObj = Object.create(null); // プロトタイプチェーンを持たないオブジェクトを作成する

console.log(noParentObj.toString); // undefined プロトタイプチェーンを持たないためtoStringメソッドも存在しない

console.log(noParentObj.hasOwnProperty); // undefined
console.log(Object.hasOwn(noParentObj, "toString")); // false Object.hasOwnはObject.prototypeに依存しないためプロトタイプチェーンを持たないオブジェクトでも利用できる
```

## 次回

[配列](https://jsprimer.net/basic/array/#array)

