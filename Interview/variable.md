# 변수

## 식별자

`문자`, `_`, `$`, `숫자`로 식별한다.

## 변수의 종류

`var a = "";` : 문자열

`var b = 0;` : 숫자

`var c = false;` : boolean

`var d = null;` : NULL

`var e = undefined;` : undefined;

`var f = [];` : 배열

`var g = {};` : 객체

`var h = function() {};` : 함수

## var , let , const

`var`는 일반적인 변수 선언 방식인데 중복되어도 값이 할당된다.

`let`은 변수 선언 방식인데 중복되면 값이 할당되지 않는다.

`const` 변수 선언 방식인데 `변수 재선언`, `변수재할당` 모두 되지 않는다.

## 변수 할당

초기값이 지정되지 않은 변수는 `undefined` 값을 갖는다.

선언되지 않은 변수에 접근하려고 하면 `Reference Error` 예외가 발생한다.
