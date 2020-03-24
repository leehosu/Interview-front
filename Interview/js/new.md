# new

객체 리터러 `{...}`을 사용하면 객체를 쉽게 만들 수 있다. 그런데 개발을 하다 보면 유사한 객체를 여러 개 만들어야 할 때가 생긴다.

`new` 연산자와 생성자 함수를 사용하면 유사한 객체를 쉽게 만들 수 있다.

## 생성자 함수

생성자 함수와 일반 함수에 기술적인 차이는 없다. 다만 생성자 함수는 아래 두 관례를 따른다.

1. 함수 이름의 첫 글자는 대문자로 시작한다.
2. 반드시 `new` 연산자를 붙여 실행한다.

```js
function User(name) {
  this.name = name;
  this.isAdmin = false;
}

let user = new User("lake");

alert(user.name); // lake
alert(user.isAdmin); // false
```

`new User(...)`를 써서 함수를 실행하면 아래와 같은 알고리즘이 동작한다.

1. 빈 객체를 만들어 `this`에 할당한다.
2. `this`에 새로운 프로퍼티를 추가해 `this`를 수정한다.
3. `this`를 반환한다.

`new User(...)`가 실행되면 무슨 일이 일어나는지 본다.

```js
function User(name) {
  // this = {}; 빈객체가 암시적으로 만들어짐

  this.name = name;
  this.isAdmin = false;

  //return this;
}
```

`new User("lake")`외에도 `new User("fire")`, `new User("Alice")`등을 이용하면 손쉽게 사용자 객체를 만들 수 있다. 객체 리터럴 문법으로 일일이 객체를 만드는 방법보다 훨씬 간단하고 읽기 쉽게 객체를 만들 수 있다.

생성자의 의의는 바로 여기에 있다. 재사용 할 수 있는 객체 생성 코드를 구현하는 것이다.

## 생성자와 return문

생성자 함수엔 보통 `return`문이 없다. 반환해야할 것들은 모두 `this`에 저장되고, `this`는 자동으로 반환되기 때문에 반환문을 명시적으로 써 줄 필요가 없다.

그런데 만약이 `return`이 있다면?

1. 객체를 `return`한다면, `this` 대신 객체가 반환된다.
2. 원시형을 `return`한다면, `return`문이 무시된다.

`return` 뒤에 객체가 오면 생성자 함수는 해당 객체를 반환해주고, 이 외의 경우는 `this`가 반환된다.

아래와 같은 예시에선 1번의 규칙이 적용되어 `return`은 `this`를 무시하고 객체를 반환한다.

```js
function BigUser() {
  this.name = "John";

  return { name: "Godzilla" };
  // this가 아닌 새로운 객체를 반환함
}

alert(new BigUser().name); // Godzilla
```

아무것도 `return`하지 않는 예시를 보면 2번째 규칙이 적용된다.

```js
function SmallUser() {
  this.name = "John";

  return; // <-- this를 반환함
}

alert(new SmallUser().name); // John
```

> 괄호 생략하기

```js
let user = new User(); // <-- 괄호가 없음
// 아래 코드는 위 코드와 똑같이 동작합니다.
let user = new User();
```

인수가 없는 생성자 함수는 괄호를 생략해 호출 할 수 있다.

## 생성자 내 메서드

생성자 함수를 사용하면 매개변수를 이용해 객체 내부를 자유롭게 구성할 수 있다.

지금까진 `this`에 프로퍼티를 더해주는 예시만 살펴봤는데, 메서드를 더해주는 것도 가능하다.

```js
function User(name) {
  this.name = name;

  this.sayHi = function() {
    alert("My name is :" + this.name);
  };
}

let lake = new User("lake");

lake.sayHi(); // my name is : lake
```

`new User(name)`은 프로퍼티 `name`과 메서드 `sayHi`를 가진 객체를 만들어준다.
