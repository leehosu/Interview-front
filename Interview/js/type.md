# Type

## Javascript type

`undefined`, `null`, `boolean`, `number`, `string`, `object`, `function`, `Array`, `Date`등이 존재한다.

## 기본형과 참조형

#### 기본형

- `number`
- `string`
- `boolean`
- `null`
- `undefined`

#### 참조형

- `object`
- `Array`
- `function`
- `RegExp`

## 기본형과 참조형의 차이점

- 기본형 : `값`을 그대로 할당
- 참조형 : `값`이 지정된 `주소`를 할당(참조)

## 정적타입과 동적 타입

#### 정적 타입

정적언어라는 자료형을 컴파일 시에 결정하는 것이다.

`C`, `C#`,`C++`,`JAVA`등의 언어가 있다. 이들 언어는 변수에 들어갈 값의 형태에 따라 자료형을 지정해줘야한다.

컴파일 시에 자료형에 맞지 않은 값이 들어있으면 컴파일 에러가 발생한다.

**장점**

- 컴파일 시에 타입에 대한 정보를 결정하기 때문에 속도가 빠르다.
- 타입 에러로 인한 문제점을 초기에 발견할 수 있어 안정성이 좋다.

#### 동적 타입

동적 타입 언어의 자료형은 컴파일 시 자료형을 정하는 것이 아니고 실행시에 결정한다.

**장점**

- Runtime까지 타입에 대한 결정을 끌고 갈 수 있기 때문에 많은 선택의 여지가 있다.

**단점**

- 실행 도중에 변수에 예상치 못한 `type`이 들어와 `TypeError`를 뿜는 경우가 생길 수 있다.
