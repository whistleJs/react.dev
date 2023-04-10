## Storing a history of moves
> 이동 기록 저장하기

If you mutated the `squares` array, implementing time travel would be very difficult.
> 만약 `squares` 배열을 변경한다면 시간 여행을 구현하는 것은 매우 어려운 일입니다.

However, you used `slice()` to create a new copy of the `squares` array after every move, and treated it as immutable. This will allow you to store every past version of the `squares` array, and navigate between the turns that have already happend.
> 그러나 모든 이동 후에 `squares` 배열을 `slice()`를 사용하여 새로운 복사본을 만들고 불변으로 취급했습니다. 이렇게 하면 `squares` 배열의 모든 과거 버전을 저장하고 이미 발생한 부분을 탐색할 수 있습니다.

You'll store the past `squares` arrays in another array called `history`, which you'll store as a new state variable. The `history` array represents all board states, from the first to the last move, and has a shape like this:
> 과거 `squares` 배열을 `history`라는 다른 배열에 저장하여 새로운 state 변수에 저장합니다. `history` 배열은 처음부터 마지막까지 모든 board state를 나타내고 다음과 같은 모양을 가지고 있습니다:

```ts
[
  // Before first move
  [null, null, null, null, null, null, null, null, null],
  // After first move
  [null, null, null, null, 'X', null, null, null, null],
  // After second move
  [null, null, null, null, 'X', null, null, null, 'O'],
  // ...
]
```