# Event Delegation

이벤트 위임(Event Delegation)이란 다수의 자식 요소에 각각 이벤트 헨들러를 바인딩 하는 대신 하나의 부모 요소에 이벤트 헨들러를 적용하는 방식이다.

```js
<ui id="todo-app">
  <li class="item"> walk </li>
  <li class="item"> tell </li>
  <li class="item"> pay </li>
</ui>
```

```js
document.addEventListener("DOMContentLoaded", function() {
  let app = document.getElementById("todo-app");
  let items = document.getElementByClassName("item");

  for (let item of items) {
    item.addEventListener("click", function() {
      alert(item.innerHTML);
    });
  }
});
```

위와 같이 `Event Listener`등록은 요소의 수가 적을때는 효율적이고 잘 돌아가지만, 요소의 갯수가 매우 많다면 매우 비효율적이다.

item 갯수마다 `Event Listener`를 생성, 등록하는 것보다 모든 list에 대해서 한 개의 `Event Listener`를 생성하여 전체를 등록하는 것이 효율적이다.

즉, 전체 아이템에 `Event Listener`를 설정하게 되면 사용자가 한 개를 선택 했을 때 해당 아이템에서 이벤트를 발생시킨다.

```js
document.addEventListener("DOMContentLoaded", function() {
  let app = document.getElementById("todo-app");

  app.addEventListener("click", function(e) {
    if (e.target && e.target.nodeName === "LI") {
      let item = e.target;
      alert(item.innerHTML);
    }
  });
});
```
