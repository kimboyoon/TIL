당장 내일이 코딩테스트인데.. OMG

# Tips

1. let 과 const 로만 쓰자

   - const만 사용해서 가능하면 그렇게 하고, 변수로 선언해야 한다면 let으로 써주자

2. 세미콜론 ;

   - 세미콜론을 항상 사용하거나 아예 사용하지 않거나 하자

3. 일치 연산자 ( == vs === )

   - == 대신, 항상 === 을 사용하자

4. 불변성 (원본 이용 vs 보존)

   - 원본을 보존하고 **깊은 복사로 값을 복사**하여 사용하자

   - 예를 들어 `sort()` 함수를 사용하면, 원본이 바뀌게 된다.

   ```js
   function sortByAges(arr) {
     arr.sort((a, b) => a.age - b.age);
   }

   // 복사해서 사용하자
   function sortByAges(arr) {
     const copyArr = arr.slice();
     copyArr.sort((a, b) => a.age - b.age);
     return copyArr;
   }
   ```

5. 삼항연산자

   - 깔끔하게 처리할 수 있을 때만 삼항연산자를 사용하자

[참고자료](https://medium.com/%EC%98%A4%EB%8A%98%EC%9D%98-%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D/%EC%9E%90%EB%B0%94%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8-%EC%BD%94%EB%94%A9-%ED%85%8C%EC%8A%A4%ED%8A%B8%EC%97%90%EC%84%9C-%EA%B0%80%EC%9E%A5-%EB%A7%8E%EC%9D%B4%ED%95%98%EB%8A%94-%EC%8B%A4%EC%88%98%EB%93%A4-a10df2c884c)

# 문제풀이 예시

## Array 중복 제거

```js
const nums = [1, 2, 3, 6, 6, 7, 2, 2, 8, 9];

const result = nums.filter((item, position) => {
  return nums.indexOf(item) === position;
});

// indexOf(item) 함수는 배열 요소 중 item인 요소의 첫번째 index 값을 리턴한다
// 예를 들어, nums 배열을 순회하다가 item 이 6일 때 첫번째 6과 두번째 6모두 indexOf(6)의 값이 3이다.
```

## 애너그램 판별하기

- 애너그램이란, 두 단어의 글자 나열 순서는 다르지만 구성이 일치할 때를 말함

```js
const stringA = "listen";
const stringB = "silent";

// 1. split(), sort(), join()
function isAnagram(strA, strB) {
  if (strA.length !== strB.length) {
    return false;
  }
  return (
    stringA
      .split("")
      .sort((a, b) => b - a)
      .join() ===
    stringB
      .split("")
      .sort((a, b) => b - a)
      .join()
  );
}
```

## 팰린드롬 / 회문

- 앞으로 or 뒤로 읽었을 때 같은 문자열인지 판별
- level => true, david => false, eye => true

```js
// 1. 추가 문자열 활용
function checkPalindrome(str) {
  let reversed = "";
  // 오른쪽에서 왼쪽 순서
  for (let i = str.length - 1; i >= 0; i--) {
    reversed += str[i];
  }
  return reversed === str;
}

// 2. Two Pointer 투포인터 활용
function checkPalindrome(str) {
  const len = str.length;
  const middle = Math.floor(len / 2);

  // charAt(인수) 는 인수번째의 문자를 리턴함. "javascript".charAt(2) 의 값은 "v" 가 된다.
  for (let i = 0; i < middle; i++) {
    if (str.charAt[i] !== str.charAt[len - 1 - i]) {
      return false;
    }
  }
  return true;
}
```

## 최대 수익 계산하기

- n 기간 동안의 주식가격 변화를 기준으로 낼 수 있는 최대 수익 계산하기
- 기간 중 가장 쌀 때 주식을 구입하고 비쌀 때 판매한다.
- 3일동안의 주식가격이 [100, 50, 250] 이라면 최대 이익은 200 (250 - 50)

```js
// 내풀이
function profit(arr) {
  let maxProfit = 0;
  let minProfit = arr[0];

  for (let i = 0; i < arr.length; i++) {
    if (arr[i] > minProfit) {
      maxProfit = arr[i] - minProfit;
    } else {
      minProfit = arr[i];
    }
  }
  return maxProfit;
}

// for of문으로 써보면
function profit(prices) {
  let maxProfit = 0;
  let minProfit = arr[0];

  for (let price of prices) {
    if (price > minProfit) {
      maxProfit = Math.max(maxProfit, price - minProfit);
    } else {
      minProfit = price;
    }
  }
  return maxProfit;
}
```

## 올바른 괄호 문제

- 반드시 짝지어서 닫혀야 함
- "()()" , "(())()" => true
- "[(])" , "(){})" => false
- **스택** 문제 : 왼쪽부터 하나씩 열린 괄호일 경우, 스택에 넣어주고 닫힌 괄호일 경우, 스택에서 제거한다. 가장 마지막에 스택에 하나도 남지 않으면 성공
- 로직
  ```js
      fn () {
          1. create Stack
          2. scan item
              3. if ("(" or "{" or "[") {
                  4. push to stack
              } else {
                  5. pop to stack
                      6. if not match item, return false
              }
          7. return stack.length === 0
      }
  ```

```js
function validParentheses(input) {
  const stack = [];
  for (char of input) {
    if (char === "(" || "{" || "[") {
      stack.push(char);
    } else {
      const lastChar = stack.pop();
      if (
        (char === ")" && lastChar !== "(") ||
        (char === "}" && lastChar !== "{") ||
        (char === "]" && lastChar !== "[")
      ) {
        return false;
      }
    }
  }
  return stack.length === 0;
}
```

## 이진 탐색 Binary Search

- 정렬된 리스트에 사용되는 탐색 알고리즘
- 리스트에서 탐색범위를 절반씩 좁혀가며 특정한 값을 찾을 때 사용
- O(logN)
- 로직
  1. Target 값이 중간값보다 작으면 중간값을 기준으로 좌측 아이템들을 탐색
  2. 중간값보다 크면 우측 아이템들을 탐색
  3. 같은 방법으로 선택된 중간값과 비교
  4. 해당 값을 찾을 때까지 반복

```js
function binarySearch(arr, target) {
  // 처음과 마지막 index
  let low = 0;
  let high = arr.length - 1;

  while (low <= high) {
    let middle = floor((low + high) / 2);
    if (target > arr[middle]) {
      low = middle + 1;
    } else if (target < arr[middle]) {
      high = middle - 1;
    } else return middle;
  }

  return -1;
}
```

## 나선형 매트릭스

## 두 객체 비교하기

- JS 특화 문제

```JS
const obj1 = {
    a: "a",
    b: 1,
    c: ["a","b","c"],
    d: {
        e: null,
        f: -1
    }
}

const obj2 = {
    a: "a",
    b: 1,
    c: ["a","b","c"],
    d: {
        e: null,
        f: -1
    }
}

obj1 === obj2 // 이렇게 비교 불가
```
- 코드 풀이

```js
// 1. 내장함수 써서 문자열로 바꿔서 사용
function isEqual(objA, objB) {
    let a = JSON.stringify(objA)
    let b = JSON.stringify(objB)

    // key, value 순서가 바뀌면 false를 반환하므로
    return a.split("").sort().join("") === b.split("").sort().join("")
}

// 2. 재귀함수 사용하여 깊숙하게 비교
function isEqual(objA, objB) {
    const checkObjects = {objA && objB && typeof objA === 'object' && typeof objB === 'object'}

    if (checkObjects && Object.keys(objA).length === Object.keys(objB).length) {
        return Object.keys(objA).reduce((equal, key) => {
            return equal && isEqual(objA[key], objB[key])
        }, true);
    } else {
        return objA === objB
    }
}
```

> 이 문제 두번째 방법은 이해하지 못했다..ㅠ
