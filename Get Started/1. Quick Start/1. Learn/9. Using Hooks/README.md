## Using Hooks
> 훅 사용하기

Functions starting with `use` are called _Hooks_. `useState` is a build-in Hook provided by React. You can find other build-in Hooks in the [API reference](https://react.dev/reference/react). You can also write your own Hooks by combining the existing ones.
> `use`로 시작하는 함수는 *Hooks*로 불립니다. `useState`는 React에서 제공하는 훅입니다. 제공하는 다른 훅을 원한다면 API reference에서 찾을 수 있습니다. 또한, 기존 훅을 결합하여 본인만의 훅을 만들 수 있습니다.  

Hooks are more restrictive than other functions. You can only call Hooks _at the top_ of your components(or other Hooks). If you want to use `useState` in a condition or a loop, extract a new component ant put it there.
> 훅은 다른 함수들보다 제한적입니다. 컴포넌트(또는 다른 훅들) 맨 위에 있는 훅들만 호출할 수 있습니다. 만약 조건문이나 반복문에서 `useState`를 사용하고 싶다면 새로운 컴포넌트로 빼서 사용해야합니다.