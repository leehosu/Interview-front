# Scope

## function scope

function 내부에서 선언한 변수는 `function scope`로 해당 함수 내에서만 접근 및 호출이 가능하다.

정의한 함수 밖에서 호출하려는 경우, 정의되지 않는 변수를 참조하려고 하여 `Reference Error` 발생

## global scope

function 밖에서 선언한 변수는 `전역 변수`로 사용되며, 해당 페이지 내의 어떤 함수에서든 접근 및 호출 할 수 있다.

```js
if (true) {
  var x = 5;
}
console.log(x);
// 5
```

```js
if (true) {
  let x = 5;
}
console.log(x);
//ReferenceError : y is not defined
```

## 할당되지 않았을 때

`undeclared` : 선언이 되지 않은 상태

`undefined` : 선언은 되었지만 초기화 되지 않은 상태 혹은 값이 없는 변수의 값

`null` : 선언을 하였고, 값을 초기화 하였으나 빈 값을 넣어놓기 원할 때 사용

## null vs undefined

둘의 차이는 `의도성`이다.

`null`은 의도적으로 빈 값을 할당하기 위해 넣어준다.
