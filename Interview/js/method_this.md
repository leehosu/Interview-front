# Method and this

객체는 사용자(user), 주문(order)등과 같이 실제 존재하는 개체(entity)를 표현하고자 할 때 생성한다.

```js
let user = {
  name: "hosu",
  age: 27
};
```

자바스크립트에선 객체의 프로퍼티에 함수를 할당하여 객체에 행동할 수 있는 능력을 부여한다.

## method

```js
let user = {
  name: "lake",
  age: 27
};

user.sayHi = function() {
  alert("hello");
};

user.sayHi(); // hello
```

함수 표현식으로 함수를 만들고, 객체 프로퍼티 `user.sayHi`에 함수를 할당하였다.

이제 객체에 할당된 함수를 호출하면 `user`가 인사를 해준다.

이렇게 객체 프로퍼티에 할당된 함수를 `method`라고 부른다.

즉, `sayHi`가 `method`가 된다.

```js
let user = {
  name: "lake",
  age: 27
};

// 함수 선언
function sayHi() {
  alert("hello");
}

// 선언된 함수를 메서드로 등록
user.sayHi = sayHi;

user.sayHi(); //hello
```

## 메서드 단축

객체 리터럴 안에 메서드를 선언할 때 사용할 수 있다.

```js
user = {
  sayHi: function() {
    alert("hello");
  }
};

user = {
  sayHi() {
    alert("hello");
  }
};
```

위의 두 객체는 동일하게 동작한다.

## method 와 this

메서드는 객체에 저장된 정보에 접근할 수 있어야 제 역할을 할 수 있다.

`user.sayHi()`의 내부 코드에서 객체 `user`에 저장된 이름(name)을 이용해 인사말을 만드는 경우가 이런 경우이다.

**메서드 내부에서 `this` 키워드를 사용하면 객체에 접근할 수 있다.**

```js
let user = {
  name: "lake",
  age: 30,

  sayHi() {
    alert(this.name);
    // this는 '현재 객체'를 나타낸다.
  }
};

user.sayHi(); // lake
```

`this`를 사용하지 않고 외부 변수를 참조하여 객체에 접근하는 것도 가능하다.

```js
let user = {
  name: "lake",
  age: 30,

  sayHi() {
    alert(user.name);
  }
};

user.sayHi(); // lake
```

이렇게 외부 변수를 사용해 객체를 참조하면 예상치 못한 에러가 발생 할 수있다.

`user`를 복사해 다른 변수에 할당(`admin = user`)하고 `user`는 전혀 다른 값으로 덮어썻다고 가정하면 `sayHi()`는 `null`을 참조할 것이다.

```js
let user = {
  name: "John",
  age: 30,

  sayHi() {
    alert(user.name);
    // Error: Cannot read property 'name' of null
  }
};

let admin = user;
user = null;
// user를 null로 덮어쓴다.

admin.sayHi();
// sayHi()가 엉뚱한 객체를 참고하면서 에러가 발생한다.
```

## this

자바스크립트의 `this`는 다른 프로그래밍 언어의 `this`와 동작 방식이 다르다.

자바스크립트에선 모든 함수에 `this`를 사용할 수 있다.

```js
function sayHi() {
  alert(this.name);
}
```

`this` 값은 런타임에 결정된다. 컨텍스트에 따라 달라진다.

동일한 함수라도 다른 객체에서 호출했다면 `this`가 참조하는 값이 달라진다.

```js
let user = { name: "lake" };
let admin = { name: "admin" };

function sayHi() {
  alert(this.name);
}

user.f = sayHi;
admin.f = sayHi;

user.f(); //lake
admin.f(); // admin
```

`obj.f()`를 호출했다면 `this`는 `f`를 호출하는 동안의 `obj`이다.

## reference type

복잡한 상황에서 메서드를 호출하면 `this`값을 잃어버리는 경우가 생긴다.

```js
let user = {
  name: "lake",
  hi() {
    alert(this.name);
  },
  bye() {
    alert("Bye");
  }
};

user.hi();

(user.name === "lake" ? user.hi : user.bye)();
// Error: Cannot read property 'name' of undefined
```

에러가 나는 원인을 파악하면,

`obj.method()`를 호출했을 때, 내부에서 어떤 일이 일어나는지 알아야 한다.

코드를 유심히 살펴보면 `obj.method()`엔 연산이 두개가 있다는 걸 알게된다.

1. `.`은 객체 프로퍼티 `obj.metho`에 접근한다.
2. `()`은 메서드를 실행한다.

`user.hi()`를 의도한 대로 동작시키기 위해 자바스크립트는 속임수를 사용한다. `.`가 함수가 아닌 `참조 타입` 값을 반환하게 한다.

참조타입은 명세에서만 사용되는 타입이다. 즉, 개발자가 실제로 사용할 수 없는 자료형이다.

## this가 없는 화살표 함수

화살표 함수는 일반 함수와 달리 고유한 `this`를 가지지 않는다. 화살표 함수에서 `this`를 참조하면, 화살표 함수가 아닌 외부 함수에서 `this`를 가져온다.

```js
let user = {
  firstName: "보라",
  sayHi() {
    let arrow = () => alert(this.firstName);
    arrow();
  }
};

user.sayHi(); // 보라
```

# 요약

- 객체 프로퍼티에 저장된 함수를 `method`라고 부른다
- `object.method()`은 객체를 사용 할 수 있게 해준다.
- 메서드는 `this`로 객체를 참조한다.
- 함수를 선언할 때 `this`를 사용 할 수 있다. 다만, 함수가 호출되기 전까지 `this`엔 값이 할당되지 않는다.
- 함수를 복사해 객체 간 전달할 수 있다.
- 함수를 객체 프로퍼티에 저장해 `object.method()` 같이 메서드 형태로 호출하면 `this`는 `object`를 참조한다.

## this 값 알아내기

```js
let object, method;

obj = {
  go: function() {
    alert(this);
  }
};

obj.go(); // [object object] - (1)

obj.go(); // [object object] - (2)

(method = obj.go)(); // undefined - (3)

(obj.go || obj.stop)(); // undefined - (4)
```

- (1) : 우리가 알고 있는 일반적인 메서드 호출 방법이다.
- (2) : 괄호가 추가되긴 했지만 연산 우선순위를 바꾸지 않으므로 `.` 연산자가 먼저 실행된다.
- (3) : `((expression).method())`이다. 이 코드는 아래와 같이 쪼갤 수 있다.

```js
f = obj.go;
f();
```

- (4) : (3)과 동일한 패턴의 호출이다. `expression`이 `obj.go || obj.stop`이라는 차이점만 있다.
