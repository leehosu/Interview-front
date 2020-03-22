# Function

## 콜백 함수

```js
function ask(question, yes, no) {
  if (confirm(question)) yes();
  else no();
}

function showOk() {
  alert("동의하셨습니다.");
}

function showCancel() {
  alert("취소 버튼을 누르셨습니다.");
}

// 사용법: 함수 showOk와 showCancel가 ask 함수의 인수로 전달됨
ask("동의하십니까?", showOk, showCancel);
```

함수 `ask`의 인수 `showOk`와 `showCancel`은 _콜백함수_ 또는 *콜백*이라고 부른다.

함수를 함수의 인자로 전달하고, 필요하다면 인수로 전달한 그 함수를 _나중에_ 호출하는것이 콜백 함수의 개념이다.

위의 예시에서는 *yes*라고 대답한 경우 `showOk`가 콜백 함수가 되고, *no*라고 대답한 경우 `showCancle`이 콜백 함수가 된다.

## 함수 표현식 vs 함수 선언식

1. 문법의 차이

**함수 표현식**

```js
let sum = function(a, b) {
  return a + b;
};
```

**함수 선언식**

```js
function sum(a, b) {
  return a + b;
}
```

2. 생성 시기의 차이
   함수 표현식은 실제 실행 흐름이 해당 함수에 도달 했을 때 함수를 생성한다.

따라서 실행 흐름이 함수에 도달했을 때 함수를 사용할 수 있다.

함수 선언문은 함수 선언문이 정의되기 전에도 호출 할 수 있다.

```js
sayHi("John"); // Hello, John

function sayHi(name) {
  alert(`Hello, ${name}`);
}
```

```js
sayHi("John"); // error!

let sayHi = function(name) {
  alert(`Hello, ${name}`);
};
```

3. scope
   엄격 모드에서 함수 선언문이 코드 블록 내에 위치하면 해당 함수는 블록 내 어디서든 접근 할 수 있다.

하지만 블록 밖에서는 함수에 접근하지 못한다.

```js
let age = prompt("나이를 알려주세요.", 18);

// 조건에 따라 함수를 선언함
if (age < 18) {
  function welcome() {
    alert("안녕!");
  }
} else {
  function welcome() {
    alert("안녕하세요!");
  }
}

// 함수를 나중에 호출한다.
welcome(); // Error: welcome is not defined
```

함수 선언문은 함수가 선언된 코드 블록 안에서만 유효하기 때문에 이런 에러가 발생한다.

```js
let age = 16; // 16을 저장했다 가정한다.

if (age < 18) {
  welcome(); // \   (실행)
  //  |
  function welcome() {
    //  |
    alert("안녕!"); //  |  함수 선언문은 함수가 선언된 블록 내
  } //  |  어디에서든 유효하다.
  //  |
  welcome(); // /   (실행)
} else {
  function welcome() {
    alert("안녕하세요!");
  }
}

// 여기는 중괄호 밖이기 때문에
// 중괄호 안에서 선언한 함수 선언문은 호출할 수 없다.

welcome(); // Error: welcome is not defined
```

```js
let age = prompt("나이를 알려주세요.", 18);

let welcome;

if (age < 18) {
  welcome = function() {
    alert("안녕!");
  };
} else {
  welcome = function() {
    alert("안녕하세요!");
  };
}

welcome(); // 제대로 동작한다.
```

지역변수로 `welcome`을 선언 후에 그 변수에 함수를 할당해주면 된다.
이것이 `함수 표현식`이다.
