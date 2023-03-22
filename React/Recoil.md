# Recoil 이란?

- Facebook 에서 만든 리액트 상태관리 라이브러리
- 가장 리액트스러우며 리액트 hooks과 사용방법이 비슷하다는 장점이 있음
- 초기세팅이 간편함 (recoil 라이브러리 설치)
- 직관적이고 단순한편

- App 전체를 `<RecoilRoot>`로 감싸고, 데이터를 Atom으로 선언하여 사용한다.

## 구성요소

1. Atom

- 하나의 상태. 리액트의 useState라고 생각하면 쉽다.
- atom의 값을 변경하면 그것을 구독하고 있는 컴포넌트들이 모두 다시 렌더링된다.
- default 값과 key 값을 설정한다.

```jsx
export const number = atom({
  key: "number",
  default: "1",
});
```

- **useRecoilState** : useState와 동일하게 사용 (값, 함수 모두 반환)
  **useRecoilValue** : 변환하는 함수 없이 atom 값만 반환
  **useSetRecoilState** : 변환하는 함수만 반환

- ex

```jsx
const [number, setNumer] = useRecoilState(number);
```

2. Selector

- 내부에서 `get`이라는 메소드를 파라미터로 받아서 사용하여 state를 가공하여 반환한다.
- 파생된 state를 나타낼 수 있다.

```jsx
const plusNumber = selector({
  key: "plusNumber",
  get: ({ get }) => {
    get(number) + 1;
  },
});
```

- atom의 userName을 가공하여 length를 받아온다.
- selector 함수로 가공된 charCountState는 쓰기가 불가능한 상태이다.
  `set` 속성을 추가하면 된다.

```js
const plusNumber = selector({
  key: "plusNumber",
  get: ({ get }) => {
    get(number) + 1;
  },
  set: ({ set }, newValue) => {
    set(number, newValue * 2);
  },
});
```
