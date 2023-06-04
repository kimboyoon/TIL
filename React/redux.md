# 키워드

## Action

상태에 변화가 필요할 때, 액션을 발생시킨다. 하나의 객체로 표현됨. `type`을 필수적으로 가지고 있어야 한다.

```js
{
    type: "ADD_TODO"
    data: {
        id: 0,
        text: "리덕스 배우기"
    }
}
```

## Action Creator

액션을 만드는 함수로 파라미터를 받아와서 액션 객체 형태로 만들어줌.

```js
export function addTodo(data) {
    return {
        type: "ADD_TODO",
        data
    }
}
```

## Reducer

변화를 일으키는 함수로 두가지의 파라미터를 받는다. 

```js
function reducer(state, action) {
    // 상태 업데이트 로직
}
```

현재의 상태와 전달 받은 액션을 참고하여 새로운 상태를 만들어서 반환한다.

```js
function counter(state, action) {
    switch (action, state) {
        case 'INCREASE':
            return state + 1;
        case 'DECREASE':
            return state - 1;
        default:
            return state;
    }
}
```

## Store

한 어플리케이션 당 하나의 스토어를 만든다. 스토어 안에는, 현재의 앱 상태, 리듀서와 추가로 내장 함수들이 있다.

## Dispatch

디스패치는 스토어의 내장함수 중 하나이다. 디스패치는 액션을 발생시키는 것. `action`을 파라미터로 전달한다.

## Subscribe

스토어의 내장함수 중 하나로 `함수 형태`의 값을 파라미터로 받는다. 


# 리덕스의 3가지 규칙

## 1. 하나의 어플리케이션 안에는 하나의 스토어가 있다.

## 2. 상태는 읽기 전용이다.

기존의 객체는 건들이지 않고 `스프레드 연산자`를 사용하여 업데이트 한다.

## 3. 리듀서는 순수한 함수여야 한다.

- 리듀서 함수는 이전 함수 `state` 와 액션 `action` 객체를 파라미터로 받는다.
- 이전 상태는 절대 건들이지 않고, 변화를 일으킨 새로운 상태 객체를 만들어서 반환한다.
- 똑같은 파라미터로 호출된 리듀서 함수는 **언제나** 똑같은 결과값을 반환한다.