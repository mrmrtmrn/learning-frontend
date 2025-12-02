# 学習メモ

## [JavaScript Primer](https://jsprimer.net/) を利用してJavaScriptの基礎を学習しなおし中
- [関数と宣言](https://jsprimer.net/basic/function-declaration/)
  - 関数の宣言の仕方は以下
    ```javascript
    function 関数名(引数1, 引数2, ...) {
      // 関数の処理
      return 戻り値;
    }
    ```
  - 定義した仮引数よりも少ない引数で呼び出した場合、足りない分の仮引数には`undefined`が設定される
  - ES2015からデフォルト引数が使える
    ```javascript
    function fn(x = "default value") {
      return x;
    }

    console.log(fn()); // "default value"
    console.log(fn("custom value")); // "custom value"
    ```
  - 定義した仮引数よりも多い引数で呼び出した場合は単純に無視される
  - `Math.max(...args)`のように任意の個数の引数を受け取れる可変長引数もある
    ```javascript
    function fn(...args) {
      // argsは配列として扱われる
      return args;
    }

    console.log(fn(1, 2, 3)); // [1, 2, 3]
    ```
  - `...`のついた引数のことをRest parameters（残余引数）と呼ぶ。配列として扱う。
  - 他の引数とRest parametersを組み合わせることもできるが、Rest parametersは必ず最後
    ```javascript
    function fn(a, b, ...rest) {
      return [a, b, rest];
    }

    console.log(fn(1, 2, 3, 4, 5)); // [1, 2, [3, 4, 5]]
    ```
  - 関数の中でのみ参照できる`arguments`という特殊な変数が存在する
  - `arguments`は配列のように扱える(`Array-like`)が、厳密には配列ではないので`Array`のメソッドは使えない
  - `arguments`は関数に渡されたすべての引数を格納している
    ```javascript
    function fn() {
      console.log(arguments[0]); // 1
      console.log(arguments[1]); // 2
    }

    fn(1, 2);
    ```
  - まあでも極力`arguments`は使わずにRest parametersを使うべき
  - 関数の引数に分割代入を使うことができる
    ```javascript
    function fn({ x, y }) {
      return x + y;
    }

    console.log(fn({ x: 1, y: 2 })); // 3
    ```
    ```javascript
    function fn([a, b]) { // 配列でもOK。この場合はプロパティ合わせるとかではなく順番どおりに値が入る
      return a * b;
    }
    console.log(fn([3, 4])); // 12
    ```
  - そもそも代入演算子(`=`)の分割代入とは以下のように左辺に定義したい変数を定義して右辺のオブジェクトの対応するプロパティを代入するもの
    ```javascript
    const obj = { a: 1, b: 2 };
    const { a, b } = obj; // a = 1, b = 2
    ```
  - JavaScriptでは関数も関数オブジェクトというオブジェクトの一種。関数名に`()`をつけて関数としてまとめた処理が呼び出される
    ```javascript
    function fn(name) {
      return `Hello, ${name}!`;
    }

    const greet = fn;
    greet("Alice"); // "Hello, Alice!"
    ```
  - ファーストクラスファンクション(第一級関数)：関数が値として扱えること
  - 関数式：関数を値として変数へ代入している式のこと
    ```javascript
    const fn = function(name) { // 関数名を省略できる(無名関数または匿名関数）
      return `Hello, ${name}!`;
    };

    console.log(fn("Bob")); // "Hello, Bob!"
    ```
  - 名前付き関数式：関数式で関数名を省略せずに定義することもできる
    ```javascript
    const fn = function greet(name) { // 関数名を省略しない
      return `Hello, ${name}!`;
    };
    console.log(fn("Charlie")); // "Hello, Charlie!"
    ```
  - 名前付き関数式の場合、関数名は関数の内部でのみ参照可能
    ```javascript
    const fn = function greet(name) {
      if (name) {
        return `Hello, ${name}!`;
      } else {
        return greet("Guest"); // 関数名を使って再帰呼び出び出しが可能
      }
    };
    console.log(fn()); // "Hello, Guest!"
    ```
  - Arrow Function(アロー関数)：ES2015で導入された書き方
    ```javascript
    const fn = (name) => {
      return `Hello, ${name}!`;
    };
    console.log(fn("Dave")); // "Hello, Dave!"
    ```
  - 引数が1つだけの場合、括弧を省略できる
    ```javascript
    const fn = name => {
      return `Hello, ${name}!`;
    };
    console.log(fn("Eve")); // "Hello, Eve!"
    ```
  - 処理が1行だけで`return`文のみの場合、中括弧と`return`を省略できる
    ```javascript
    const fn = name => `Hello, ${name}!`;
    console.log(fn("Frank")); // "Hello, Frank!"
    ```
  - 以下のようにコールバック関数を渡す場合に便利
    ```javascript
    const numbers = [1, 2, 3, 4, 5];

    const doubled = numbers.map(n => n * 2);　// Arrow Functionの場合
    
    const doubled = numbers.map(function(n) { // 通常の関数式の場合
      return n * 2;
    });
    
    console.log(doubled); // [2, 4, 6, 8, 10]
    ```
  - アロー関数で書けるならアロー関数のほうがいいらしい
    - なんか`this`の扱いが違うらしい。別の章で解説されるっぽい。
  - 関数名が被った場合は後勝ちになる
    - 仮引数の数が違っても関係ない
      ```javascript
      function greet() {
        return "Hello!";
      }

      function greet(name) {
        return `Hello, ${name}!`;
      }
      console.log(greet()); // "Hello, undefined!"
      console.log(greet("Grace")); // "Hello, Grace!"
      ```
  - 関数の上書きを避けたい場合にはconstで関数式を使うとエラーが発生するので意図しない上書きを防げて良い
    ```javascript
    const greet = function(name) {
      return `Hello, ${name}!`;
    };

    // constは同じ変数名で再宣言できないので構文エラー
    const greet = function(name) {
      return `Hi, ${name}!`;
    };
    ```
  - 引数として渡される関数のことをコールバック関数と呼ぶ。コールバック関数を引数として使う関数のことを高階関数と呼ぶ。
    ```javascript
    function 高階関数(コールバック関数) {
      // 何らかの処理
      コールバック関数(); // コールバック関数を呼び出す
    }
    ```
  - メソッド：オブジェクトのプロパティとして定義された関数のこと
    ```javascript
    const obj = {
      greet: function(name) {
        return `Hello, ${name}!`;
      },
      greetArrow: name => `Hello, ${name}!`,
      shortGreet(name) { // ES2015以降の省略記法
        return `Hello, ${name}!`;
      }
    };

    console.log(obj.greet("Hank")); // "Hello, Hank!"
    console.log(obj.greetArrow("Ivy")); // "Hello, Ivy!"
    ```
## 次回

[文と式](https://jsprimer.net/basic/statement-expression/#statement-and-expression)