# 学習メモ

## [JavaScript Primer](https://jsprimer.net/) を利用してJavaScriptの基礎を学習しなおし中

### [配列](https://jsprimer.net/basic/array/#array)

```javascript
const array = [1, 2, 3]; // 配列リテラル
console.log(array.length); // 要素数知りたい時
console.log(array[9999]); // undefined

const includeUndefinedArray = [1, , 3]; // 要素の省略も可能。省略された要素はundefinedになる。要素を持っているとは限らない。疎な配列っていうらしい。
console.log(includeUndefinedArray.length); // 3
console.log(includeUndefinedArray[1]); // undefined

// 疎な配列と密な配列は一見区別がつかない
const denseArray = [1, undefined, 3]; // 明示的にundefinedを入れた密な配列
const sparseArray = [1, , 3]; // 要素を省略した疎な配列
console.log(denseArray[1]); // undefined
console.log(sparseArray[1]); // undefined
console.log(Object.hasOwn(sparseArray, 1)); // false 疎な配列の省略された要素はプロパティとして存在しない
console.log(Object.hasOwn(denseArray, 1)); // true 密な配列の要素はプロパティとして存在する
```

```javascript
const array = [1, 2, 3, 4, 5];

// 最後の要素にアクセスするとき
console.log(array[array.length - 1]); // 5
console.log(array.at(-1)); // 5 [ES2022]からはatメソッドを使うと負のインデックスで後ろからアクセスできる
console.log(array[-1]); // undefined 配列のインデックスに負の数を指定してもundefinedになるので注意
```

```javascript
// Array型の判定はArray.isArrayを使う
console.log(Array.isArray([])); // true
console.log(Array.isArray({})); // false
console.log(typeof []); // "object" 配列はオブジェクトの一種なのでtypeofでは区別できない
```

固定長かつ同じ型の要素を持つ配列が必要な場合はTypedArrayを使う。
文字列や数値のプリミティブ型の値を直接扱えないので普段はあまり使わないかも？
```javascript
const int8Array = new Int8Array(3); // 長さ3のInt8Arrayを作成
console.log(Array.isArray(int8Array)); // false TypedArrayは配列ではない
```

```javascript
const array = [1, 2, 3];
const [first, second, third] = array; // 分割代入で配列の要素を取り出せる
console.log(first); // 1
console.log(second); // 2
console.log(third); // 3
```

```javascript
const array = ["a", "b", "c", "d", "e", "c"];

// インデックスの値がほしい時
console.log(array.indexOf("c")); // =>2 配列の中から値が"three"の要素のインデックスを探す
console.log(array.lastIndexOf("c")); // =>5 配列の中から値が"three"の要素のインデックスを後ろから探す

console.log(array.indexOf("x")); // =>-1 配列の中に値が"x"の要素が存在しない場合は-1が返る
console.log(array.lastIndexOf("x")); // =>-1 配列の中に値が"x"の要素が存在しない場合は-1が返る

const obj = { id: 2 };
const includeObjectArray = [{ id: 1 }, obj, { id: 3 }, obj];
console.log(includeObjectArray.indexOf({ id: 1 })); // =>-1 リテラルは新しいオブジェクトを作るので見つからない
console.log(includeObjectArray.indexOf(obj)); // =>1 これだといける
console.log(includeObjectArray.lastIndexOf(obj)); // =>3 これもOK

// オブジェクトとしては異なるけど値は同じものを探したい場合はfindIndexメソッドを使う
console.log(includeObjectArray.findIndex(item => item.id === 2)); // =>1
console.log(includeObjectArray.findLastIndex(item => item.id === 2)); // =>3

// 要素自体が欲しい場合はfindメソッドを使う
console.log(includeObjectArray.find(item => item.id === 2)); // =>{ id: 2 }
console.log(includeObjectArray.findLast(item => item.id === 2)); // =>{ id: 2 } あまり例として良くない。例えば数値プロパティを持ってるようなオブジェクトが複数あって、値が10以上のやつ〜みたいな検索かけたりするのがいい例かも
console.log(includeObjectArray.find(item => item.id === 9999)); // =>undefined 見つからない場合はundefinedが返る

// 配列を範囲指定して新しい配列を作成するsliceメソッド.
console.log(array.slice(1, 4)); // =>["b", "c", "d"] インデックス1から4まで(4は含まない)の要素を抽出して新しい配列を作成する
console.log(array.slice(1)); // =>["b", "c", "d", "e", "c"] 第二引数を省略すると第一k引数のインデックス1から最後までの要素を抽出して新しい配列を作成する
console.log(array.slice(-3)); // =>["d", "e", "c"] 負のインデックスも指定できる。これは後ろから3つの要素を抽出して新しい配列を作成する
console.log(array.slice(1,1)); // =>[] 第一引数と第二引数が同じ場合は空配列が返る
console.log(array.slice(4,1)); // =>[] 第一引数が第二引数より大きい場合も空配列が返る

// 含まれているかどうかの真偽値を得たい場合はincludesメソッドを使う
console.log(array.includes("c")); // =>true
console.log(array.includes("x")); // =>false
// オブジェクトの場合は参照が同じかどうかで判定される
console.log(includeObjectArray.includes(obj)); // =>true
console.log(includeObjectArray.includes({ id: 2 })); // =>false
// オブジェクトの値が同じかどうかを判別するときはsomeで対応する
console.log(includeObjectArray.some(item => item.id === 2)); // =>true
console.log(includeObjectArray.some(item => item.id === 9999)); // =>false
```

```javascript
const array = [1, 2, 3];
array.push(4); // 配列の末尾に要素を追加する
console.log(array); // [1, 2, 3, 4]
const poppedValue = array.pop(); // 配列の末尾の要素を取り出して削除する
console.log(poppedValue); // 4
console.log(array); // [1, 2, 3]

array.unshift(0); // 配列の先頭に要素を追加する
console.log(array); // [0, 1, 2, 3]
const shiftedValue = array.shift(); // 配列の先頭の要素を取り出て削除する
console.log(shiftedValue); // 0
console.log(array); // [1, 2, 3]

const addedArray = array.concat([4, 5]); // 配列を結合して新しい配列を作成する.別に配列を渡さなくてもarray.concat(4)のようにしてもOK
console.log(addedArray); // [1, 2, 3, 4, 5]
console.log(array); // [1, 2, 3] 元の配列は変更されない

// ...(スプレッド構文)を使って配列リテラル中に既存の配列を展開することもできる
const spreadedArray = [0, ...array, 4, 5];
console.log(spreadedArray); // [0, 1, 2, 3, 4, 5]
```

任意の位置に要素を削除・追加したいときは`Array.prototype.splice`メソッドを使う。
```javascript
const array = [1, 2, 3, 4, 5];
array.splice(2, 1); // インデックス2から1個要素を削除する
console.log(array); // [1, 2, 4, 5]

array.splice(0, array.length); // すべての要素を削除する
console.log(array); // []

const array2 = [1, 2, 3, 4, 5];
array2.length = 0; // lengthプロパティに0を代入してもすべての要素を削除できる
console.log(array2); // []
```

JavaScriptではメソッド名から破壊的/非破壊的かを判別するのが難しいので都度確認するようにする
配列を引数として受け取るような関数の中で配列を操作する場合には特に注意が必要
```javascript
const array = [1, 2, 3];
array.splice(1, 1); // インデックス1から1個要素を削除する
console.log(array); // arrayは[1, 3]となり、これは破壊的なメソッドとなる

const array2 = [1, 2, 3];
console.log(array2.toSpliced(1, 1)); // インデックス1から1個要素を削除した新しい配列を返す
console.log(array2); // array2は元のまま[1, 2, 3]となり、非破壊的なメソッドとなる
```

```javascript
const array = [1, 2, 3];
array.forEach((element, index, array) => {
  // 配列の各要素に対して一度ずつ実行される関数を指定する
  console.log(`要素:${element}, インデックス:${index}`);
});

const mappedArray = array.map((element, index, array) => {
  // 配列の各要素に対して一度ずつ実行される関数を指定し、その戻り値から新しい配列を作成する
  return element * 2;
});
console.log(mappedArray); // [2, 4, 6]

const filteredArray = array.filter((element, index, array) => {
  // 配列の各要素に対して一度ずつ実行される関数を指定し、その戻り値がtrueとなる要素から新しい配列を作成する
  return element % 2 === 1; // 奇数だけ抽出する
});
console.log(filteredArray); // [1, 3]

const reducedValue = array.reduce((accumulator, currentValue, currentIndex, array) => {
  // 配列の各要素に対して一度ずつ実行される関数を指定し、その戻り値を次の要素の処理に引き継いで最終的に1つの値を返す
  return accumulator + currentValue;
}, 0); // 第二引数で初期値を指定できる。省略した場合は配列の最初の要素が初期値になる
console.log(reducedValue); // 6
```

```javascript
const array = [[[1], 2], 3];
console.log(array.flat()); // [ [ 1 ], 2, 3 ] 深さ1で配列を平坦化する
console.log(array.flat(1)); // [ [ 1 ], 2, 3 ] 深さ1で配列を平坦化する
console.log(array.flat(2)); // [ 1, 2, 3 ] 深さ2で配列を平坦化する
console.log(array.flat(Infinity)); // [ 1, 2, 3 ] 深さ無制限で配列を平坦化する
```

```javascript
const array = [1, 2, 3];
const doubled = array.flatMap(element => [element, element * 2]); // 各要素を2倍にした配列を作成し、それを1段階平坦化して新しい配列を作成する。つまりmapしてからflat。
console.log(doubled); // [1, 2, 2, 4, 3, 6]
```

```javascript
const array = [1, 2, 3, 4, 5];
const grouped = Object.groupBy(array, element => (element % 2 === 0 ? "even" : "odd")); // 配列の各要素を指定した関数でグループ化してオブジェクトとして返す
console.log(grouped); // { odd: [ 1, 3, 5 ], even: [ 2, 4 ] }
```

## 次回

[文字列](https://jsprimer.net/basic/string/)

