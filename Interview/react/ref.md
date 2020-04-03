# Ref

> React에서 Ref 사용하기

- `React`에서는 `Component`에서 `props` 사용을 통해서 `DOM` 노드에 레퍼런스를 걸지 않고도 `UI` 제어가 가능하다.
- `React Ref`는 특정한 `DOM` 노드, 혹은 `Component`에 `reference`를 걸어주는 것이다.
- `Ref`를 통해서 `render` 메서드에서 만든 `DOM` 노드나 `React` 요소에 접근해서 값을 수정할 수 있다.

## Ref의 값

노드의 타입마다 `ref`값이 다르다.

`React`의 `ref 문서`에 따르면 두개의 케이스가 있다.

1. HTML 요소에 ref attribute를 전달하면 DOM 노드가 current 속성 값이 된다.
2. react 요소인 component에 ref를 쓰면 mount된 component의 값이 current 속성 값이 된다.

_함수형 component에서는 인스턴스가 없기 때문에 `ref`를 줄 수 없다._

## Ref를 쓰는 시기

- DOM 노드에 접근해서 focus, media 재생 등을 제어하거나 사이즈를 얻어 올 때
- 애니메이션을 직접 실행시킬 때
- 서드 파티 라이브러리를 사용할 때
- 자식의 state에 부모가 접근할 때
- state로 제어하지 않는 비제어 component에 사용할 때
