## Lifting state up
> state 올리기

Currently, each `Square` component maintains a part of the game's state. To check for a winner in a tic-tac-toe game, the `Board` would need to somehow know the state of each of the 9 `Square` components.
> 현재, 각 `Square` 컴포넌트는 게임의 state 일부를 유지합니다. tic-tac-toe 게임에서 우승자를 확인하려면, `Board`는 9개 `Square` 컴포넌트의 각 state를 알아야 합니다.  

How would you approach that?
> 어떻게 접근할 수 있을까요?

At first, you might guess that the `Board` needs to "ask" each `Square` for that `Square`'s state.
먼저, `Board`는 각 `Square`에 `Square`의 state을 "물어"볼 필요가 있을 것입니다.

Although this approach is technically possible in React, we discourage it because the code becomes difficult to understand, susceptible to bus, and hard to refactor. Instead, the best approach is to store the game's state in the parent `Board` component instead of in each `Square`. The `Board` component can tell each `Square` what to display by passing a prop, like you did when you passed a number to each Square.
이러한 접근 방식은 React에서 기술적으로는 가능하지만 코드를 이해하기 어렵고 취약하며 유지보수하기에 어려워집니다. 가장 좋은 접근 방법은 각 `Square` 대신에 부모인 `Board` 컴포넌트에 게임의 state를 저장하는 것입니다. `Board` 컴포넌트는 각 Square에 prop을 전달하여 표시할 내용을 각 Square에 알려줄 수 있습니다.

**To collect data from multiple children, or to have child components communicate with each other, declare the shared state in their parent component instead. The parent component can pass that state back down to the children via props. This keeps the child components in sync with each other and with their parent.**
> **여러 하위 컴포넌트에서 데이터를 수집하거나 하위 컴포넌트가 서로 통신하려면, 부모 컴포넌트에 state를 대신 정의합니다. 부모 컴포넌트는 하위 컴포넌트에 prop으로 state를 전달할 수 있습니다. 이렇게 하면 하위 컴포넌트가 부모 컴포넌트와 동기화됩니다.**  

Lifting state into a parent component is common when React components are refactored.
> React 컴포넌트를 리팩토링할 때 부모 컴포넌트로 올리는 state는 일반적입니다.

Let's take this opportunity to try it out. Edit the `Board` component so that it declares a state variable named `squares` that defaults to an array of 9 nulls corresponding to the 9 squares:
> 이번 기회에 한 번 해보도록 하겠습니다. `Board` 컴포넌트를 변경해서 9개의 사각형에 전달할 9개의 null 배열을 기본값으로 하는 `squares`라는 변수를 정의했습니다:

```tsx
// ...
export default function Board() {
  const [squares, setSquares] = useState(Array(9).fill(null));
  return (
    // ...
  );
}
```

`Array(9).fill(null)` creates an array with nine elements and sets each of them to `null`. The `useState()` call around it declares a `squares` state variable that's initially set to that array. Each entry in the array corresponds to the value of a square. When you fill the board in later, the `squares` array will look like this:
> `Array(9).fill(null)`은 9개의 요소를 가진 배열을 생성하고 각 요소들을 `null`로 설정해줍니다. `useState()`로 감싸서 호출하면 해당 배열이 초기값인 `squares` state 변수가 정의됩니다. 배열의 각 요소는 `square`의 value에 해당됩니다. board를 채우고 나면, `squares` 배열은 이렇게 볼 수 있습니다:

```ts
['0', null, 'X', 'X', 'X', 'O', 'O', null, null]
```

Now your `Board` component need to pass the `value` prop down to each `Square` that it renders:
> 이제 `Board` 컴포넌트는 `value` prop으로 렌더링하는 각 `Square` 컴포넌트에 전달해야합니다.

```tsx
export default function Board() {
  const [squares, setSquares] = useState(Array(9).fill(null));
  return (
    <>
      <div className="board-row">
        <Square value={squares[0]} />
        <Square value={squares[1]} />
        <Square value={squares[2]} />
      </div>
      <div className="board-row">
        <Square value={squares[3]} />
        <Square value={squares[4]} />
        <Square value={squares[5]} />
      </div>
      <div className="board-row">
        <Square value={squares[6]} />
        <Square value={squares[7]} />
        <Square value={squares[8]} />
      </div>
    </>
  );
}
```

Next, you'll edit the `Square` component to receive the `value` prop from the Board component. This will require removing the Square component's own stateful tracking of `value` and the button's `onClick` prop:
> 다음에, Board 컴포넌트로부터 `value` prop을 받을 수 있도록 `Square` 컴포넌트를 수정해야 합니다. Square 컴포넌트가 가지고 있는 `value` state와 button의 `onClick` prop을 지워야합니다.

```tsx
function Square({value}) {
  return <button className="square">{value}</button>;
}
```

At this point you should see and empty tic-tac-toe board:
> 이 시점에서 비어 있는 tic-tac-toe 게임판을 볼 수 있습니다:

<img src="https://user-images.githubusercontent.com/42595869/229732457-0c5b2b75-2297-4ff4-ab62-64031d109eff.png" width="300" height="auto">

And your code should look like this:
> 그리고 코드는 이렇게 볼 수 있습니다:

```tsx
import { useState } from 'react';

function Square({ value }) {
  return <button className="square">{value}</button>;
}

export default function Board() {
  const [squares, setSquares] = useState(Array(9).fill(null));
  return (
    <>
      <div className="board-row">
        <Square value={squares[0]} />
        <Square value={squares[1]} />
        <Square value={squares[2]} />
      </div>
      <div className="board-row">
        <Square value={squares[3]} />
        <Square value={squares[4]} />
        <Square value={squares[5]} />
      </div>
      <div className="board-row">
        <Square value={squares[6]} />
        <Square value={squares[7]} />
        <Square value={squares[8]} />
      </div>
    </>
  );
}
```

<img src="https://user-images.githubusercontent.com/42595869/229732901-23855d17-4bf9-4da1-a9f2-9ad00fb417f3.png" width="800" height="auto">

Each Square will now receive a `value` prop that will either be `'X'`, `'O'`, or `null` for empty squares.
> 각 Square은 `'X'`, `'O'` 또는 비어있는 상태를 나타내는 `null`을 `value` prop으로 받을 수 있게 되었습니다.

Next, you need to change what happends when a `Square` clicked. The `Board` component now maintains which squares are filled. You'll need to create a way for the `Square` to update the `Board`'s state. Since state is private to a component that defines it, you cannot update the `Board`'s state directly from `Square`.
> 다음은 `Square`가 클릭되었을 때 값을 바꿔줘야합니다. `Board` 컴포넌트가 사각형을 채우는 것을 유지합니다. `Square`가 `Board`의 state를 바꾸는 방법을 만들어야 합니다. state는 컴포넌트에서 정의한 개인 정보이기 때문에 `Square`에서 `Board`의 state를 직접 변경할 수 없습니다.  

Instead, you'll pass down a function from the `Board` component to the `Square` component, and you'll have `Square` call that function when a square is clicked. You'll start with the function that the `Square` component will call when it is clicked. You'll call that function `onSquareClick`:
> 대신에 `Board` 컴포넌트에서 `Square` 컴포넌트로 함수를 넘기고 클릭했을 때 `Square`에서 함수를 호출하면 됩니다. `Square` 컴포넌트가 클릭되었을 때 해당 함수에서 시작합니다. 그 함수를 `onSquareClick`로 부릅시다:  

```tsx
function Square({ value }) {
  return (
    <button className="square" onClick={onSquareClick}>
      {value}
    </button>
  );
}
```

Next, you'll add the `onSquareClick` function to the `Square` component's props:
> 다음에 `Square` 컴포넌트의 prop으로 `onSquareClick` 함수를 추가합니다:

```tsx
function Square({ value, onSquareClick }) {
  return (
    <button className="square" onClick={onSquareClick}>
      {value}
    </button>
  );
}
```

Now you'll connect the `onSqureClick` prop to a function in the `Board` component that you'll name `handleClick`. To connect `onSquareClick` to `handleClick` you'll pass a function to the `onSquareClick` prop of the first `Square` component:
> 이제 `onSquareClick` prop을 `Board` 컴포넌트의 `handleClick` 함수랑 연결합니다. `onSquareClick`을 `handleClick`과 연결하려면 첫번째 `Square` 컴포넌트의 `onSquareClick` prop으로 함수를 전달합니다:

```tsx
export default function Board() {
  const [squares, setSquares] = useState(Array(9).fill(null));

  return (
    <>
      <div className="board-row">
        <Square value={squares[0]} onSquareClick={handleClick} />
        //...
  );
}
```

Lastly, you will define the `handleClick` function inside the Board component to update the `squares` array holding your board's state:
> 마지막으로 Board 컴포넌트 내부의 `handleclick` 함수를 정의하여 board의 state인 `squares` 배열을 업데이트합니다

```tsx
export default function Board() {
  const [squares, setSquares] = useState(Array(9).fill(null));

  function handleClick() {
    const nextSquares = squares.slice();
    nextSquares[0] = "X";
    setSquares(nextSquares);
  }

  return (
    // ...
  );
}
```

The `handleClick` function creates a copy of the `squares` array (`nextSquares`) with the JavaScript `slice()` Array method. Then, `handleClick` updates the `nextSquares` array to add `x` to the first (`[0]` index) square.
> `handleClick` 함수에서 Javascript `slice()` 배열 메소드를 사용하여 `squares` 배열(`nextSqusares`)을 새로 복사했습니다. 그리고 `handleClick`은 `nextSquares` 배열의 첫번째(`[0]` index)를 `x`를 추가하여 변경했습니다.  

Calling the `setSquares` function lets React know the state of the component has changed. This will trigger a re-render of the components that use the `squares` state (`Board`) as well as its child components(the `Square` components that make up the board).
> `setSquares` 함수를 호출하면 React는 컴포넌트의 state가 바뀐다는 것을 압니다. 그러면 `squares` state(`Board`)를 사용하는 하위 컴포넌트(board에서 만들어진 `Square` 컴포넌트)가 다시 렌더링됩니다.  

Now you can add X's to the board... but only to the upper left square. Your `handleClick` function is hardcoded to update the index for the upper left square(`0`). Let's update `handleClick` to be able to update any square. Add an argument `i` to the `handleClick` function that takes the index of the square to update:
> 이제 board에 X를 추가할 수 있지만... 왼쪽 상단 square만 추가할 수 있습니다. `handleClick` 함수는 왼쪽 상단 square(`0`)만 변경할 수 있도록 하드 코딩되어 있습니다. 어느 사각형이든 사용할 수 있도록 `handleClick`을 변경합시다. `handleClick` 함수에 인수 `i`를 추가하여 square의 index를 가져올 수 있도록 변경합니다:  

```tsx
export default function Board() {
  const [squares, setSquares] = useState(Array(9).fill(null));

  function handleClick(i) {
    const nextSquares = squares.slice();
    nextSquares[i] = "X";
    setSquares(nextSquares);
  }

  return (
    // ...
  );
}
```

Next, you will need to pass that `i` to `handleClick`. You would try to set the `onSquareClick` prop of square to be `handleClick(0)` directly in the JSX like this, but it won't work:
> 다음, `handleClick`에 `i`를 전달해주어야 합니다. JSX에서 직접 `onSquareClick` prop을 `handleClick(0)`으로 설정할 수 있지만 작동하지 않습니다:  

```tsx
<Square value={squares[0]} onSquareClick={handleClick(0)} />
```

Here is why this doesn't work. The `handleClick(0)` call will be a part of rendering the board component. Because `handleClick(0)` alters the state of the board component by calling `setSquares`, your entire board component will be re-rendered again. But this runs `handleClick(0)` again, leading to an infinite loop:
> 왜 작동하지 않는지 봅시다. `handleClick(0)`를 호출하는 것은 board 컴포넌트 렌더링의 일부입니다. 왜냐하면 `handleClick(0)`는 `setSquares`를 호출하여 board 컴포넌트의 state를 변경할 것이고 board 컴포넌트는 다시 렌더링 될 것입니다. 하지만 또한 `handleClick(0)`가 다시 호출되고 무한 루프에 빠지게 됩니다:

<img src="https://user-images.githubusercontent.com/42595869/230011374-5185682d-1a53-42e5-ba38-5610a2544975.png" width="800" height="auto">

Why didn't this problem happen earlier?
> 왜 이 문제가 더 빠르게 나타나지 않았을까요?

When you were passing `onSquare={handleClick}`, you were passing the `handleClick` function down as a prop. You were not calling it! But now you are _calling_ that function right away-notice the parentheses in `handleClick(0)`-and that's why it runs too early. You don't want to call `handleClick` until the user clicks!
> `onSquare={handleClick}`으로 전달할 때, `handleClick` 함수를 prop으로 전달한겁니다. 우리는 호출하지 않았습니다! 하지만 이제는 `handleClick(0)`에서 괄호를 묶고 *호출*하고 너무 일찍 실행되고 있습니다. 우리는 사용자가 클릭하기 전까지 `handleClick`을 호출하고 싶지 않습니다!

You could fix by creating a function like `handleFirstSquareClick` that calls `handleClick(0)`, a function like `handleSecondSquareClick` that calls `handleClick(1)`, and so on. You would pass (rather than call) these functions down as props like `onSquareClick={handleFirstSquareClick}`. This would solve the infinite loop.
> `handleClick(0)`을 호출하는 `handleFirstSquareClick`, `handleClick(1)`을 호출하는 `handleSecondSquareClick` 등과 같은 함수를 생성하여 고칠 수 있습니다. 이러한 함수는 `onSquareClick={handleFirstSquareClick}`처럼 prop으로 함수를 전달(호출 대신에)할 수 있습니다. 무한 루프도 해결됩니다.

However, defining nine different funcitons and giving each of them a name is too verbose. Instead, let's do this:
> 그러나 9개의 다른 함수를 정의하고 전달하는 것은 너무 많습니다. 대신에 이렇게 합시다:

```tsx
export default function Board() {
  // ...
  return (
    <>
      <div className="board-row">
        <Square value={squares[0]} onSquareClick={() => handleClick(0)} />
        // ...
  );
}
```

Notice the new `() =>` syntax. Here, `() => {handleClick(0)}` is an _arrow function_, which is a shorter way to define functions. When the square is clicked, the code after the `=>` "arrow" will run, calling `handleClick(0)`.
> 새로운 문법 `() =>`를 봅시다. `() => {handleClick(0)}`은 함수를 짧게 정의할 수 있는 *arrow function*입니다. 사각형이 클릭됐을 때, `=>` "arrow" 뒤에 있는 코드인 `handleClick(0)`이 호출됩니다.  

Now you need to update the other eight squares to call `handleClick` from the arrow functions you pass. Make sure that the argument for each call of the `handleClick` corresponds to the index of the correct square:
> 이제 arrow function을 사용하여 다른 8개 square에도 `handleClick`을 호출할 수 있도록 변경해야 합니다. 각 `handleClick`에 대한 호출의 인수가 올바른 square index와 일치하는지 확인합니다.  

```tsx
export default function Board() {
  // ...
  return (
    <>
      <div className="board-row">
        <Square value={squares[0]} onSquareClick={() => handleClick(0)} />
        <Square value={squares[1]} onSquareClick={() => handleClick(1)} />
        <Square value={squares[2]} onSquareClick={() => handleClick(2)} />
      </div>
      <div className="board-row">
        <Square value={squares[3]} onSquareClick={() => handleClick(3)} />
        <Square value={squares[4]} onSquareClick={() => handleClick(4)} />
        <Square value={squares[5]} onSquareClick={() => handleClick(5)} />
      </div>
      <div className="board-row">
        <Square value={squares[6]} onSquareClick={() => handleClick(6)} />
        <Square value={squares[7]} onSquareClick={() => handleClick(7)} />
        <Square value={squares[8]} onSquareClick={() => handleClick(8)} />
      </div>
    </>
  );
}
```

Now you can again add X's to any square on the board by clicking on them:
> 이제 다시 board의 어떠한 사각형을 클릭하면 X를 추가할 수 있습니다.

<img src="https://react.dev/images/tutorial/tictac-adding-x-s.gif" width="300" height="auto">

But this time all the state management is handled by the `Board` component!
> 하지만 `Board` 컴포넌트에서 모든 state를 관리하고 있습니다!

This is what your code should look like:
> 코드는 이렇게 보일겁니다:

```tsx
import { useState } from 'react';

function Square({ value, onSquareClick }) {
  return (
    <button className="square" onClick={onSquareClick}>
      {value}
    </button>
  );
}

export default function Board() {
  const [squares, setSquares] = useState(Array(9).fill(null));

  function handleClick() {
    const nextSquares = squares.slice();
    nextSquares[i] = 'X';
    setSquares(nextSquares);
  }

  return (
    <>
      <div className="board-row">
        <Square value={squares[0]} onSquareClick={() => handleClick(0)} />
        <Square value={squares[1]} onSquareClick={() => handleClick(1)} />
        <Square value={squares[2]} onSquareClick={() => handleClick(2)} />
      </div>
      <div className="board-row">
        <Square value={squares[3]} onSquareClick={() => handleClick(3)} />
        <Square value={squares[4]} onSquareClick={() => handleClick(4)} />
        <Square value={squares[5]} onSquareClick={() => handleClick(5)} />
      </div>
      <div className="board-row">
        <Square value={squares[6]} onSquareClick={() => handleClick(6)} />
        <Square value={squares[7]} onSquareClick={() => handleClick(7)} />
        <Square value={squares[8]} onSquareClick={() => handleClick(8)} />
      </div>
    </>
  );
}
```

<img src="https://user-images.githubusercontent.com/42595869/230017183-75c1966c-c2bb-444d-95e7-21bfbcb370d8.png" width="800" height="auto">

Now that your state handling is in the `Board` component, the parent `Board` component passes props to the child `Square` components so that they can be displayed correctly. When clicking on a `Square`, the child `Square` component now asks the parent `Board` component to update the state of the board. When the `Board`'s state changes, both the `Board` component and every child `Square` re-renders automatically. Keeping the state of all squares in the `Board` component will allow it to determine the winner the feature.
> 이제 `Board` 컴포넌트에서 state를 관리하므로 부모 `Board` 컴포넌트는 하위 `Square` 컴포넌트에 prop으로 전달하여 올바르게 표시될 수 있습니다. `Square`를 클릭할 때, 하위 `Square` 컴포넌트는 부모 `Board` 컴포넌트에게 board의 state를 변경할 수 있도록 요청합니다. `Board`의 state가 변경될 때, `Board` 컴포넌트와 모든 하위 `Square`는 자동적으로 다시 렌더링됩니다. `Board` 컴포넌트에 모든 square의 state를 유지하면 승자를 결정하는 기능을 만들 수 있습니다.

Let's recap what happens when a user clicks the top left square on your board to add an `X` to it:
> 사용자가 board의 왼쪽 상단 사각형을 클릭하여 `X`를 추가할 때 어떤 일이 발생하는지 요약하겠습니다:

1. Clicking on the upper left square runs the function that the `button` received as its `onClick` prop from the `Square`. The `Square` component received that function as its `onSquareClick` prop from the `Board`. The `Board` component defined that function directly in the JSX. It calls `handleClick` with an argument of `0`.
> 1. 왼쪽 상단 사각형을 클릭하면 `Square`에 `button`이 `onClick` prop으로 받은 함수를 실행합니다. `Square` 컴포넌튼 `Board`에서부터 `onSquareClick` 함수를 받았습니다. `Board` 컴포넌트는 JSX에서 직접 함수를 정의했습니다. 인수 `0`과 함께 `handleClick`을 호출합니다.

2. `handleClick` uses the argument(`0`) to update the first element of the `squares` array from `null` to `X`.
> 2. `handleClick`은 인수(`0`)을 사용하여 `squares` 배열의 첫번째 요소를 `null`에서 `X`로 변경합니다.

3. The `squares` state of the `Board` component was updated, so the `Board` and all of its children re-render. This causes the `value` prop of the `Square` component with index `0` to change from `null` to `X`.
> 3. `Board` 컴포넌트의 `squares` state가 변경되면 `Board`와 모든 하위 컴포넌트가 다시 렌더링됩니다. 이로 인해 index가 `0`인 `Square` 컴포넌트의 `value` prop은 `null`에서 `X`로 변경됩니다.

In the end the user sees that the upper left square has changed from empty to having a `X` after clicking it.
> 왼쪽 상단 사각형을 클릭하면 비어있는 값에서 `X`로 변경된 것을 확인할 수 있습니다.