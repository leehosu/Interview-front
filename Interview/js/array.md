# Array and Method

배열은 다양한 `method`를 제공한다.

## 배열 탐색하기

#### indexOf, lastIndexOf , includes

- `arr.indexOf(item,from)`는 인덱스 `from`부터 시작해 `item`을 찾는다. 요소를 발견하면 해당 요소의 인덱스를 반환하고, 발견하지 못했으면 `-1`을 반환한다.
- `arr.lastIndexOf(item,from)`는 위 메서드와 동일한 기능을 하는데, 검색을 끝에서부터 시작한다.
- `arr.includes(item,from)`는 인덱스 `from`부터 시작해 `item`이 있는지를 검색하는데, 해당하는 요소를 발견하면 `true`를 반환한다.

```js
let arr = [1, 0, false];

console.log(arr.indexOf(0)); // 1
console.log(arr.indexOf(fasle)); // 2
console.log(arr.indexOf(null)); // -1
console.log(arr.indcludes(1)); // true
```

위 메서드들은 요소를 찾을 때 완전 항등 연산자 `===`을 사용한다.

요소의 위치를 정확히 알고 싶은게 아니고 요소가 배열 내 존재하는지 여부만 확인하고 싶다면 `arr.includes`를 사용하는 것이 좋다.

#### find와 findIndex

객체로 이루어진 배열이 있다면 특정 조건에 부합하는 객체를 배열 내에서 찾는 방법이다.

```js
let result = arr.find(function(item, index, array) {
  // true가 반환되면 반복을 멈추고 해당 요소를 반환한다.
  // 조건에 해당하는 요소가 없으면 undefined를 반환한다.
});
```

- `item` : 함수를 호출할 요소
- `index` : 요소의 인덱스
- `array` : 배열 자기 자신

```js
let users = [
  { id: 1, name: "lake" },
  { id: 2, name: "bob" },
  { id: 3, name: "alice" }
];

let user = users.find(item => item.id == 1);
console.log(user.name);
// lake
```

#### filter

`find` 메서드는 함수의 반환 값을 `true`로 만드는 단 하나의 요소를 찾는다.

조건을 충족하는 요소가 여러 개라면 `arr.filter`를 사용하면 된다.

`filter`는 `find`와 문법이 유사하지만, 조건에 맞는 요소 전체를 담는 배열을 반환한다는 점에서 차이가 있다.

```js
let results = arr.filter(function(item, index, array) {
  // 조건을 충족하는 요소는 results에 순차적으로 더한다.
  // 조건을 충족하는 요소가 하나도 없으면 빈 배열이 반환된다.
});
```

```js
let users = [
  { id: 1, name: "lake" },
  { id: 2, name: "bob" },
  { id: 3, name: "alice" }
];

// 앞쪽 사용자 두 명을 반환합니다.
let someUsers = users.filter(item => item.id < 3);

console.log(somUsers.length);
// 2
```

## 배열을 변형하는 메서드

#### map

`arr.map`은 유용성과 사용 빈도가 아주 높은 메서드이다.
`map`은 배열 요소 전체를 대상으로 함수를 호출하고, 함수 호출 결과를 배열로 반환한다.

```js
let result = arr.map(function(item, index, array) {
  // 요소 대신 새로운 값을 반환한다.
});
```

```js
let lengths = ["Bilbo", "Gandalf", "Nazgul"].map(item => item.length);
alert(lengths);
// 5,7,6
```

위의 예시에서는 각 요소의 길이를 출력해준다.

#### sort(fn)

`arr.sort()`는 배열의 요소를 정렬해준다. 배열 자체가 변경된다.

메서드를 호출하면 재정렬된 배열이 반환되는데, 이미 `arr`자체가 수정되기 때문에 반환값은 사용하지 않는다.

```js
arr.sort((a, b) => a - b);
```

#### split과 join

메시지 전송 어플리케이션을 만든다고 가정해보자. 수신자가 여러 명일 경우, 발신자는 쉼표로 각 수신자를 구분한다. 개발자는 긴 물자열 형태의 수신자 리스트를 배열 형태로 전환해 처리하고 싶다.

그럴때 `str.split(delim)`을 이용한다. 이 메서드는 구분자(delimiter)을 기준으로 문자열을 쪼갠다.

```js
let names = "Bilbo, Gandalf, Nazgul";

let arr = names.split(", ");

for (let name of arr) {
  alert(`${name}에게 보내는 메시지`);
  // Bilbo에게 보내는 메시지
}
```

`split` 메서드는 두번째 인수로 숫자를 받을 수 있다. 이 숫자는 배열의 길이를 제한해주므로 길이를 넘어서는 요소를 무시할 수 있다.

```js
let arr = "Bilbo, Gandalf, Nazgul, Saruman".split(", ", 2);

alert(arr); // Bilbo, Gandalf
```

`join`은 `split`과 반대 역할을 하는 메서드이다. 인수를 접착체 처럼 사용해 배열 요소를 모두 합친 후 하나의 문자열을 만든다.

```js
let arr = ["Bilbo", "Gandalf", "Nazgul"];

let str = arr.join(";");
// 배열 요소 모두를 ;를 사용해 하나의 문자열로 합친다.

alert(str);
// Bilbo;Gandalf;Nazgul
```

#### reduce와 reduceRight

`reduce`와 `reduceRight`는 배열을 기반으로 값 하나를 도출 할 때 사용한다.

**문법**

```js
let value = arr.reduce(
  function(accumulator, item, index, array) {
    // ...
  },
  [init]
);
```

인수로 넘겨주는 함수는 배열의 모든 요소를 대상으로 적용되는데, 적용 결과는 다음 함수 호출 시 사용된다.

**함수의 인수**

- `accumulator` : 이전 함수 호출의 결과
- `item` : 현재 배열의 위치
- `index` : 요소의 위치
- `array` : 배열
- `init` : 함수 최초 호출시 사용되는 초깃값(옵션)

첫번째 인수는 앞서 호출했던 함수들의 결과가 누적되어 저장되고 마지막 함수까지 호출 되면 이 값은 `reduce`의 반환값이 된다.

```js
let arr = [1, 2, 3, 4, 5];

let result = arr.reduce((sum, current) => sum + current, 0);

console.log(result);
// 15
```

1. 함수 최초 호출시, `reduce`의 마지막 인수인 `0`이 `sum`에 할당된다. `current`엔 배열의 첫 번째 요소인 `1`이 할당된다.
2. 두 번째 호출시, `sum=1`이고 여기에 배열의 두 번째 요소인 `2`가 더해지므로 결과는 `3`이 된다.

위와 같은 과정이 계속 이어진다.

```js
let arr = [1, 2, 3, 4, 5];

let result = arr.reduce((sum, current) => sum + current);

console.log(result);
// 15
```

사실 위와 같이 초기값을 생략해도 된다.

## 배열 메서드와 `thisArg`

함수를 호출하는 대부부의 배열 메서드 (`find`, `filter`, `map`등)는 `thisArg`라는 매개변수를 옵션으로 받을 수 있다.

```js
arr.find(func, thisArg);
arr.filter(func, thisArg);
arr.map(func, thisArg);
// ...
// thisArg는 선택적으로 사용할 수 있는 마지막 인수이다.
```

`thisArg`는 `func`의 `this`가 된다.
