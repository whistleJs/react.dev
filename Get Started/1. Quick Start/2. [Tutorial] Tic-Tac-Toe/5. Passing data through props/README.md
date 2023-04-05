## Passing data through props
> props를 통해 데이터 넘기기

Next, you'll want to change the value of a square from empty to "X" when the user clicks on the square. With how you've built the board so far you would need to copy-paste the code that updates the square nine times(once for each square you have)! Instead of copy-pasting, React's component architecture allows you to create a resuable component to avoid messy, duplicated code.
> 다음, 비어있던 사각형을 클릭했을 때 "X"로 값을 바꾸길 원합니다. 지금까지 게임판을 만들었던 방법으로 사각형 값을 변경하는 코드를 9번 복사-붙여넣기하면 됩니다(각 사각형마다 한 번씩). 복사-붙여넣기 대신에 React 컴포넌트 구조는 지저분하고 중복된 코드를 방지하기 위해 재사용할 수 있는 컴포넌트를 만들 수 있도록 허용합니다.

First, you are going to copy the line defining first square (`<button className="square">1</button>`) from your `Board` component into a new `Square` component:
> 먼저, 첫번째 사각형(`<button className="square">1</button>`)을 복사하여 `Board` 컴포넌트 안에 넣을 새로운 `Square` 컴포넌트를 정의합니다.

```tsx
function Square() {
  return <button className="square">1</button>;
}

export default function Board() {
  // ...
}
```

Then you'll update the Board component to render that `Square` component using JSX syntax:
> 이제 JSX 문법을 사용한 `Square` 컴포넌트를 렌더링할 수 있도록 Board 컴포넌트를 업데이트합니다:

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

Note how unlike the browser `div`s, your own components `Board` and `Square` must start with a capital letter.
> 브라우저에서 `div`와 다르게 컴포넌트는 `Board`와 `Square`와 같이 대문자로 시작해야 합니다.

Let's take a look:
> 이제 확인해봅시다:

<img src="https://user-images.githubusercontent.com/42595869/229296999-8291bf9f-676e-4417-ae2f-c790a4469157.png" width="300" height="auto">

Oh no! You lost the numbered squares you had before. Now each square says "1". To fix this, you will use _props_ to pass the value each square should have from the parent component(`Board`) to its child(`Square`).
> 오 이런! 사각형에 번호를 매기는 것을 잊어버렸습니다. 지금은 각 사각형마다 "1"를 보여주고 있습니다. 이것을 고치려면 부모 컴포넌트(`Board`)에서 자식 컴포넌트(`Square`)에게 *prop*를 사용하여 값을 넘겨주어야 합니다.

Update the `Square` component to read the `value` prop that you'll pass from the `Board`:
> `Board`로부터 `value` prop으로 읽을 수 있도록 `Square` 컴포넌트를 변경합니다:

```tsx
function Square({ value }) {
  return <button className="square">1</button>
}
```

`function Square({ value })` indicates the Square component can be passed a prop called `value`.
> `function Square({ value })`는 Square 컴포넌트가 prop으로부터 `value`를 사용할 수 있도록 명시합니다.

Now you want to display that instead of `1` inside every square. Try doing it like this:
> 이제 모든 사각형 안에 `1` 대신 원하는 값이 표시됩니다. 이렇게 시도해보세요:

```tsx
function Square({ value }) {
  return <button className="square">value</button>;
}
```

Oops, this is not what you wanted:
> 앗, 이건 우리가 원한게 아닙니다:

<img src="https://user-images.githubusercontent.com/42595869/229301374-06f77b32-8922-4ed9-a0a8-f4aa05b67d5c.png" width="300" height="auto">

You wanted to render the JavaScript variable called `value` from your component, not the word "value". To "escape into JavaScript" from JSX, you need curly braces. Add curly braces around `value` in JSX like so:
> 우리가 원하는 것은 "value" 단어가 아닌 JavaScript 변수 `value`를 컴포넌트에서 호출해서 렌더링하는 것입니다. JSX에서 "escape into JavaScript"를 하려면 중괄호를 사용해야합니다. JSX에서 `value` 양쪽에 중괄호를 추가합니다:

```tsx
function Square({ value }) {
  return <button className="square">{value}</button>;
}
```

For now, you should see an empty board:
> 지금은 비어있는 게임판을 볼 수 있습니다:

<img src="https://user-images.githubusercontent.com/42595869/229301576-11ecf25c-5285-4d06-942a-8749c707c1b0.png" width="300" height="auto">

This is because the `Board` component hasn't passed the `value` prop to each `Square` component it renders yet. To fix it you'll add the `value` prop to each `Square` component rendered by the `Board` component:
> 왜냐면 `Board` 컴포넌트에서 각 `Square` 컴포넌트에 `value` prop으로 값을 아직 넘겨주지 않았기 때문입니다. `Board` 컴포넌트에서 각 `Square` 컴포넌트에 `value` prop을 추가하여 고칠 수 있습니다.

```tsx
export default function Board() {
  return (
    <>
      <div className="board-row">
        <Square value="1" />
        <Square value="2" />
        <Square value="3" />
      </div>
      <div className="board-row">
        <Square value="4" />
        <Square value="5" />
        <Square value="6" />
      </div>
      <div className="board-row">
        <Square value="7" />
        <Square value="8" />
        <Square value="9" />
      </div>
    </>
  );
}
```

Now you should see a grid of numbers again:
> 이제 다시 그리드 형태인 숫자를 볼 수 있습니다:

<img src="https://user-images.githubusercontent.com/42595869/229301781-3557622f-7aa4-4523-ad51-caed550e5df5.png" width="300" height="auto">

Your updated code should look like this:
> 변경된 코드는 이렇게 보이면 됩니다:

```tsx
function Square({ value }) {
  return <button className="square">{value}</button>;
}

export default function Board() {
  return (
    <>
      <div className="board-row">
        <Square value="1" />
        <Square value="2" />
        <Square value="3" />
      </div>
      <div className="board-row">
        <Square value="4" />
        <Square value="5" />
        <Square value="6" />
      </div>
      <div className="board-row">
        <Square value="7" />
        <Square value="8" />
        <Square value="9" />
      </div>
    </>
  );
}
```

<img src="https://user-images.githubusercontent.com/42595869/229301861-88c9d5df-6941-4bac-9901-637cb6a8a86d.png" width="800" height="auto">