# Closure

`closure`은 내부 함수가 `scope`밖에 있는 변수에 접근 하는 것이다.

Q. 정수 값을 갖는 list를 반복문으로 접근하여 해당 요소를 3초 지연시키고 값을 출력하라.

```js
const arr = [10,20,30,40];

for(var i = 0 ; i < arr.length;i++){
  setTimeout(function(){
      console.log("index :" + i );
    }), 3000);
};
```
위의 방법은 모두 4가 출력된다.

문제의 원인은 `setTimeout` 함수가 `i`를 반복하는 `scope`밖의 `scope`를 갖는 `closure`를 생성하기 때문이다.

```js

const arr = [10,20,30,40];
for(let i = 0 ; i < arr.length; i++){
  setTimeout(function() {
    console.log("index:" + i);
  },3000);
}
```
위의 방법은 `let`으로 할당하여 현재 `scope`내에서 i의 ㄱ밧이 바인딩되는 코드이다.

