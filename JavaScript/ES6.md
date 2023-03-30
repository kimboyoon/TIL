# ES6 ?

ECMAScript 2015 는 ES6 or ECMAScript 6 라고 한다.

## 기능

1. let

- `Block Scope` 변수 선언 가능
- 재선언 불가, 재할당 가능

2. const

- 상수 선언 키워드
- 값을 변경할 수 없다

3. Arrow Functions

- 화살표 함수
- 기존 함수 작성법보다 간결하게 표현 가능

```js
function add(a, b) {
  return a + b;
}

const add = (a, b) => {
  return a + b;
};

// 생략형 (함수 안에 return문만 있는 경우)
const add = (a, b) => a + b;
```

4. 스프레드(...) 연산자

- 객체나 배열 안의 요소들을 **복사**에 이용
- 자기 자신은 영향X

```js
const numbers = [1, 3, 5, 7];
const result = [...numbers].map(x => x + 1);
// numbers = [1, 3, 5, 7]
// result = [2, 4, 6, 8]
```

5. 템플릿 리터럴

- 백틱(`)을 이용하여 **문자열 안에 변수를 넣는** 방법
- (+) 를 사용하는 것보다 가독성이 좋다

```js
let name = '보윤'
let age = 26
let str = `제 이름은 ${name}이고, ${age}세 입니다`
console.log(str) // 제 이름은 보윤이고 26세입니다
```

6. Destructing

- 구조 분해 할당
```js
const developer = {
    name: 'boyoon',
    age: 26,
}

// 구조분해할당 안했을 때
const name = developer.name;
const age = developer.age;
console.log(name, age) // boyoon 26

// 구조분해할당
const { name, age } = developer;
console.log(name, age) // boyoon 26
```

7. for of 문
```js
const arr = [1, 3, 5];

for (const value of arr) {
    console.log(value);
} 

// 1
// 3
// 5
```