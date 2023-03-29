## Updating the screen
> 화면 업데이트하기

Often, you'll want your component to "remember" some information and display it. For example, maybe you want to count the number of times a button is clicked. To do this, add _state_ to your component.
> 종종 우리는 컴포넌트가 정보를 "기억"하고 표시하길 원합니다. 예를 들어, 버튼을 클릭한 횟수를 계산하기 원합니다. 이렇게 하려면, 컴포넌트에 *state*를 추가하면 됩니다.

First, import `useState` from React:
> 첫번째, React로부터 `useState`를 불러오세요:

```typescript
import { useState } from 'react';
```

Now you can declare to _state variable_ inside your component:
> 이제 컴포넌트에서 *state 변수*를 선언할 수 있습니다.

```tsx
function MyButton() {
  const [count, setCount] = useState(0);
```

You'll get two things from `useState`: the current state(`count`), and the function that lets you update it(`setCount`). You can give them any names, but the convention is to write `[something, setSomething]`.
> `useState`로부터 2가지를 알 수 있습니다: 현재 상태(`count`)와 업데이트를 할 함수(`setCount`). 아무 이름을 부여할 수 있지만 `[something, setSomething]`을 약속하고 있습니다.  

The first time the button is displayed, `count` will be `0` because you passed `0` to `useState()`. When you want to change state, call `setCount()` and pass the new value to it. Clicking this button will increment the counter:
> 처음 버튼을 표시할 때 `useState()`에 `0`을 넣어주었기 때문에 `count`는 `0`으로 선언되었습니다. state를 바꾸길 원할 때 `setCount()`에 새로운 값을 넣어 호출하면 됩니다. 클릭하면 증가하는 카운터입니다:


```tsx
function MyButton() {
  const [count, setCount] = useState(0);

  function handleClick() {
    setCount(count + 1);
  }

  return (
    <button onClick={handleClick}>
      Clicked {count} times
    </button>
  );
}
```

React will call your component function again. This time, `count` will be `1`. Then it will be `2`. And so on.
> React는 컴포넌트 함수를 다시 호출합니다. 이번에는 `count`는 `1`이 됩니다. 그 다음에는 `2`가 됩니다.

If you render the same component multiple times, each will get its own state. Click each button separately:
> 만약 같은 컴포넌트를 여러 개 표시하게 된다면 state가 각각 생기게 됩니다. 각 버튼 따로 클릭하기:

```tsx
import { useState } from 'react';

export default function MyApp() {
  return (
    <div>
      <h1>Counters that update separately</h1>
      <MyButton />
      <MyButton />
    </div>
  );
}

function MyButton() {
  const [count, setCount] = useState(0);

  function handleClick() {
    setCount(count + 1);
  }

  return (
    <button onClick={handleClick}>
      Clicked {count} times
    </button>
  );
}
```

<img src="https://user-images.githubusercontent.com/42595869/228606545-094c0ea0-502d-41b3-9f7f-8ec9edeb38b7.png" width="800" height="auto">

Notice how each button "remembers" its own `count` state and doesn't affect other buttons.
> 각 버튼은 `count` state를 기억하고 다른 버튼에 영향을 주지 않습니다.
