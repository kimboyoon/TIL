# var vs let vs const

## let vs const

let은 바뀌는 값 선언할 떄,

const는 바뀌지않는 값 선언할 때 사용


## var vs let

1. `var`
    - 함수 안에서 선언하면 local scope
    - 블록 안에서 선언하면 global scope

2. `let`
    - 함수 안에서 선언하면 local scope
    - 블록 안에서 선언하면 block scope


## var vs let vs const

||var|let|const|
|:---------:|:---:|:---:|:---:|
|**global scope**|O|X|X|
|**script scope**|X|O|O|
|**functional local scope**|O|O|O|
|**block scope**|X|O|O|
|**재선언**|O|X|X|
|**재할당**|O|O|X|