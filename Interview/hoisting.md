# 호이스팅

`호이스팅`이란 Javascript 변수가 `scope` 최상단으로 끌어올려지는 것을 의미한다.

## 변수 호이스팅

```js
console.log(x === undefined); // true
var x = 3;
```

```js
var myvar = "my value";

(function() {
  console.log(myvar); // undefined
  var myvar = "local value";
})();
```

`호이스팅`이 일어나도 끌어올려진 변수를 출력하면 여전히 `undefined`를 출력한다.

```js
var x;
console.log(x === undefined); // true
x = 3;
```

```js
var myVar = "value";
(function() {
  console.log(myVar);
  var myVar = "local";
})();
```

- 심지어 이 변수를 사용 혹은 참조를 하여도 여전히 `undefined`를 반환한다.

## 함수 호이스팅

```js
foo(); //bar

function foo() {
  console.log("bar");
}
```

함수에서는 단지 함수 선언식만 `호이스팅` 된다.

```js
foo(); //TypeError : foo is not a function

var foo = function() {
  console.log("bar");
};
```

함수 표현식은 `호이스팅`이 일어나지 않는다.
