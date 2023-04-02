## Making an interactive component
> 상호작용 컴포넌트 만들기

Let's fill the `Square` component with an `x` when you click it. Declare a function called `handleClick` inside of the `Square`. Then, add `onClick` to the props of the button JSX element returned from the `Square`:
> 클릭했을 때 `Square` 컴포넌트에 `x`를 채우도록 합니다. `Square` 안에 `handleClick` 함수를 정의합니다. 이제 `Square` 컴포넌트에 있는 버튼 JSX 요소에 `onClick` prop를 추가합니다.

```tsx
function Square({ value }) {
  function handleClick() {
    console.log('clicked!');
  }

  return (
    <button
      className="square"
      onClick={handleClick}
    >
      {value}
    </button>
  );
}
```

If you click on a square now, you should see a log saying `"clicked!"` in the _Console_ tag at the bottom of the _Browser_ section in CodeSandbox. Clicking the square more than once will log `"clicked!"` again. Repeated console logs with the same mesage will not create more lines in the console. Instead, you will see an incrementing counter next to your first `"clicked!"` log.  
> 이제 사각형을 클릭한다면 CodeSandbox 아래에 *Browser* 섹션의 *Copnsole* 태그에서 `"clicked!"`가 나타나는 것을 확인할 수 있습니다. 사각형을 다시 클릭하면 `"clicked!"`가 나타나는 것을 확인할 수 있습니다. console에서 추가적인 라인을 생성하지 않고 같은 메세지를 되짚고 있습니다. 대신에 `"clicked!"` 로그에 카운터가 증가하는 것을 볼 수 있습니다.

<br />

As a next step, you want the Square component to "remember" that it got clicked, and fill it with an "X" mark. To "remember" things, components use _state_.
> 다음 단계에서는 Square 컴포넌트가 클릭된 것을 "기억"하고 "X" 표시를 채우도록 하겠습니다. 컴포넌트는 *state*를 사용해서 이러한 것들을 "기억"합니다.  

React provides a special function called `useState` that you can call from your component to let it "remember" things. Let's store the current value of the `Square` in state, and change it when the `Square` is clicked.
> React는 `useState`로 불리는 특별한 함수를 제공하는데 컴포넌트에서 호출하여 "기억"할 수 있게 할 수 있습니다. `Square` 안의 state에 현재 값을 저장하고 `Square`를 클릭했을 때 변경할 수 있도록 합니다.  

Import `useState` at the top of the file. Remove the `value` prop from the `Square` component. Instead, add a new line at the start of the `Square` that calls `useState`. Have it return a state variable called `value`:
> 파일 상단에 `useState`를 추가합니다. `Sqaure` 컴포넌트에서 `value` prop을 지웁니다. 대신에, `Square` 컴포넌트에서 시작하는 새로운 라인에 `useState`를 호출합니다. `value`라는 state 변수를 반환하도록 합니다.

```tsx
import { useState } from 'react';

function Square() {
  const [value, setValue] = useState(null);

  function handleClick() {
    // ...
}
```

`value` stores the value and `setValue` is a function that can be used to change the value. The `null` passed to `useState` is used as the initial value for this state variable, so `value` here starts off equal to `null`.
> `value`는 값을 저장하고 `setValue`는 값을 변경할 수 있도록하는 함수입니다. `useState`에 `null` 넘겨 이 state 변수의 초기값을 설정해줘서 `value`는 `null`과 동일하게 시작합니다.

Since the `Square` component no longer accepts props anymore, you'll remove the `value` prop from all nine of the Square components created by the Board component:
> `Square` 컴포넌트는 더이상 prop을 사용하기 않기 때문에 Board 컴포넌트에서 생성하여 9개의 Square 컴포넌트에 넘겨주는 `value` propt을 지웁니다.

```tsx
// ...
export default function Board() {
  return (
    <>
      <div className="board-row">
        <Square />
        <Square />
        <Square />
      </div>
      <div className="board-row">
        <Square />
        <Square />
        <Square />
      </div>
      <div className="board-row">
        <Square />
        <Square />
        <Square />
      </div>
    </>
  );
}
```

Now you'll change `Square` to display an "X" when clicked. Replace the `console.log("clicked!");` event handler with `setValue('X');`. Now your `Square` component looks like this:
> 이제 `Square`를 클릭했을 때 "X"가 표시되도록 변경합시다. `console.log("clicked!");`를 `setValue('X');`로 변경합니다. 이제 `Square` 컴포넌트를 이렇게 보이게 됩니다:

```tsx
function Square() {
  const [value, setValue] = useState(null);

  function handleClick() {
    setValue('X');
  }

  return (
    <button
      className="square"
      onClick={handleClick}
    >
      {value}
    </button>
  );
}
```

By calling this `set` function from an `onClick` handler, you're telling React to re-render that `Square` whenever its `<button>` is clicked. After the update, the `Square`'s `value` will be `'X'`, so you'll see the "X" on the game board. Click on any Square, and "X" should show up:
> `onClick` 핸들러에 있는 `set` 함수를 호출함으로써, React의 `<button>`을 클릭할 떄마다 `Square`를 다시 렌더링하게 전달합니다. 변경 후, `Square`의 `value`는 '`X`'가 되어서 게임판에서 "X"를 볼 수 있을 것입니다. 어떠한 Square를 클릭해도 "X"를 볼 수 있습니다:

<img src="https://react.dev/images/tutorial/tictac-adding-x-s.gif" width="300" height="auto">

Each Square has is own state: the `value` stored in each Square is completely independent of the others. When you call a `set` function in a component, React automatically updates the child components inside too.
> 각 Square는 state를 가지고 있습니다: 각 Square에 저장된 `value`는 완전히 독립적입니다. 컴포넌트의 `set` 함수를 호출할 때, React는 자동적으로 하위 컴포넌트도 변경하게 합니다.

After you've made the above changes, your code will look like this:
> 위에서 변경한 후의 코드는 다음과 같습니다:

```tsx
import { useState } from 'react';

function Square() {
  const [value, setValue] = useState(null);

  function handleClick() {
    setValue('X');
  }

  return (
    <button
      className="square"
      onClick={handleClick}
    >
      {value}
    </button>
  );
}

export default function Board() {
  return (
    <>
      <div className="board-row">
        <Square />
        <Square />
        <Square />
      </div>
      <div className="board-row">
        <Square />
        <Square />
        <Square />
      </div>
      <div className="board-row">
        <Square />
        <Square />
        <Square />
      </div>
    </>
  );
}
```

<img src="https://user-images.githubusercontent.com/42595869/229333420-a49ae518-b93a-4d15-9045-e0bf932df822.png" width="800" height="auto">