# useEffect

## useEffext 안에서의 return문?

- 정리(clean-up)가 필요한 경우 사용

- [dep] 값이 없는 경우, return 해주는 함수가 컴포넌트 componentWillUnmount 함수와 같다. (**unmount 될 때**)

> unmount란? 컴포넌트가 사라질때

- [dep] 값이 있는 경우, 해당 **useEffect가 실행되기 전** clean-up 함수가 실행된다.

- 성능을 최적화할 수 있다