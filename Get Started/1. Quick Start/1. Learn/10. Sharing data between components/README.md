## Sharing data between components
> 컴포넌트끼리 데이터 공유하기

In the previous example, each `MyButton` had its own independent `count`, and when each button was clicked, only the `count` for the button clicked changed.
> 이전 예제에서 각 `MyButton` 컴포넌트는 독립적인 `count`를 가지고 있고 버튼이 클릭되었을 때 클릭된 버튼의 `count`만 변경되었습니다.

<div style="display: flex;">
  <img src="https://user-images.githubusercontent.com/42595869/228720925-79a1807e-4724-4d3e-89fc-2a24d2ff8adc.png" width="400" height="auto">
  <img src="https://user-images.githubusercontent.com/42595869/228721121-b3159248-e02b-4770-854b-c9fe664e1715.png" width="400" height="auto">
</div>

However, often you'll need components to _share data and always update together_.
> 그러나 종종 *데이터를 공유하고 항상 같이 업데이트*되는 컴포넌트가 필요할 때가 있습니다.

To make both `MyButton` components display the same `count` and update together, you need to move the state from the individual buttons "upwards" to the closest component containing all of them.
> 두 개의 `MyButton` 컴포넌트에 동일한 `count`가 표시되고 같이 업데이트하려면 state를 모든 버튼들을 포함하고 있는 가장 가까운 "상위" 컴포넌트로 이동시켜야 합니다.

In this example, it is `MyApp`:
> `MyApp` 예제에서:

<div style="display: flex">
  <img src="https://user-images.githubusercontent.com/42595869/228722306-406a0845-886e-413d-9fb7-931ce341be39.png" width="400" height="auto">
  <img src="https://user-images.githubusercontent.com/42595869/228722317-f1857bf0-b748-4850-ad1e-07dff927189c.png" width="400" height="auto">
</div>

Now when you click either button, the `count` in `MyApp` will change, which will change both of the counts in `MyButton`. Here's how you can express this in code.
> 둘 중 아무 버튼을 클릭할 때, `MyButton`의 count를 변경합니다. 이것을 코드로 표현다면 다음과 같습니다.

First, _move the state up_ from `MyButton` into `MyApp`:
> 첫번째, `MyButton`에서 `MyApp`으로 *state를 위로 올립니다*:

```tsx
export default function MyApp() {
  const [count, setCount] = useState(0);

  function handleClick() {
    setCount(count + 1);
  }

  return (
    <div>
      <h1>Counters that update separately</h1>
      <MyButton />
      <MyButton />
    </div>
  );
}

function MyButton() {
  // ... we're moving code from here ...
}
```

Then, _pass the state down_ from `MyApp` to each `MyButton`, together with the shared click handler. You can pass information to `MyButton` using the JSX curly braces, just like you previously did with built-in tags like `<img>`:
> 그리고 `MyApp`에서 각 `MyButton`으로 클릭 핸들러도 같이 *state를 넘겨서* 공유합니다. 이전에 `<img>`와 같은 기본 태그를 사용한 것과 같이 JSX 중괄호를 사용하여 `MyButton`에 정보를 넘겨줄 수 있습니다.

```tsx
export default function MyApp() {
  const [count, setCount] = useState(0);

  function handleClick() {
    setCount(count + 1);
  }

  return (
    <div>
      <h1>Counters that update together</h1>
      <MyButton count={count} onClick={handleClick} />
      <MyButton count={count} onClick={handleClick} />
    </div>
  );
}
```

The information you pass down like this is called _props_. Now the `MyApp` component contains the `count` state and the `handleClick` event handler, and _passes both of them down as props_ to each of the buttons.
> 정보를 아래로 넘겨주는 것을 *props*라고 부릅니다. 이제 `MyApp` 컴포넌트에 state `count`와 이벤트 핸들러 `handleClick`를 포함하고 있고 각 버튼들에 *props로 모두 넘겨줍니다*.

Finally, change `MyButton` to _read_ the props you have passed from its parent component:
> 마침내, `MyButton` 부모 컴포넌트로부터 전달받은 prop들을 *읽기* 형태로 변환합니다.

```tsx
function MyButton({ count, onClick }) {
  return (
    <button onClick={onClick}>
      Clicked {count} times
    </button>
  );
}
```

When you click the button, the `onClick` handler fires. Each button's `onClick` prop was set to the `handleClick` function inside `MyApp`, so the code inside of it runs. That code calls `setCount(count + 1)`, incrementing the `count` state variable. The new `count` value is passed as a prop to each button, so they all show the new value. This is called "lifting state up". By moving state up, you've shared it between components.
> 버튼을 클릭했을 때, `onClick` 핸들러가 작동합니다. 각 버튼들의 `onClick` prop은 `MyApp` 안의 `handleClick` 함수로 설정되어서 해당 코드가 실행됩니다. `setCount(count + 1)`코드를 호출하는 것인데, `count` state 변수를 증가시킵니다. 새로운 `count` 값은 각 버튼 prop으로 넘겨줘서 새로운 값을 보여주게 됩니다. 이것을 "lifting state up"으로 부릅니다. state를 위로 이동하면, 컴포넌트끼리 공유할 수 있습니다.

```tsx
import { useState } from 'react';

export default function MyApp() {
  const [count, setCount] = useState(0);

  function handleClick() {
    setCount(count + 1);
  }

  return (
    <div>
      <h1>Counters that update together</h1>
      <MyButton count={count} onClick={handleClick} />
      <MyButton count={count} onClick={handleClick} />
    </div>
  );
}

function MyButton({ count, onClick }) {
  return (
    <button onClick={onClick}>
      Clicked {count} times
    </button>
  );
}
```

<img src="https://user-images.githubusercontent.com/42595869/228728419-a4882d10-e2c5-4512-9175-f56dd645b43f.png" width="800" height="auto">