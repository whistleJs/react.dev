## Building the board
> 게임판 만들기

Let's get back to `App.js`. This is where you'll spend the rest of the tutorial.
> `App.js`로 돌아가봅시다. 여기서 튜토리얼의 나머지 시간을 보낼 수 있습니다.

Currently the board is only a single square, but you need nine! If you just try and copy paste your square to make two squares like this:
> 현재 게임판은 사각형 하나밖에 없지만 9개가 필요합니다!. 만약 사각형을 복사 붙여넣기로 2개를 만들면 이렇게 됩니다:

```tsx
export default function Square() {
  return <button className="square">X</button><button className="square">X</button>;
}
```

You'll get this error:
> 그러면 이러한 에러를 보게됩니다.

<img src="https://user-images.githubusercontent.com/42595869/229287285-c55e3b18-8d20-4bcc-8b09-df79ee110ef6.png" alt="/src/App.js: Adjacent JSX elements must be wrapped in an enclosing tag. Did you want a JSX fragment <>...</>?" width="800" height="auto">

React components need to return a single JSX element and not multiple adjacent JSX elements like two  buttons. To fix this you can use _fragments_ (`<>` and `</>`) to wrap multiple adjacent JSX elements like this:
> React 컴포넌트들은 두 개의 버튼처럼 여러 JSX 요소가 아닌 단일 JSX 요소를 반환해야 합니다. 여러개의 JSX 요소를 감싸는 *fragment* (`<>`와 `</>`)를 사용하여 고칠 수 있습니다:  

```tsx
export default function Square() {
  return (
    <>
      <button className="square">X</button>
      <button className="square">X</button>
    </>
  );
}
```

Now you should see:
> 이제 이렇게 볼 수 있습니다:

<img src="https://user-images.githubusercontent.com/42595869/229287464-1c72a09b-7422-4ddb-ad7b-234ed74e73e8.png" width="200" height="auto">

Great! Now you just need to copy-paste a few times to add nine squares and...
> 좋습니다! 이제 복사-붙여넣기를 여러 번 반복하여 9개의 사각형을 만들고...

<img src="https://user-images.githubusercontent.com/42595869/229287609-2d357df9-6f3f-4f5d-a9c1-1f6153761418.png" width="800" height="auto">

Oh no! The squares are all in a single line, not in a grid like you need for our board. To fix this you'll need to group your squares into rows with `div`s and some CSS classes. While you're at it, you'll give each square a number to make sure you know where each square is displayed.
> 오 이런! 사각형들이 우리가 원하는 그리드 형태와 같지 않고 단일 라인으로 있습니다. 사각형을 `div`와 CSS 클래스가 있는 행으로 묶어서 해결할 수 있습니다. 각 사각형이 표시되는 위치를 확실히 알 수 있도록 번호를 부여하겠습니다.  

In the `App.js` file, update the `Square` component to look like this:
> `App.js` 파일에서 `Square` 컴포넌트를 다음과 같이 바꿉니다: 

```tsx
export default function Square() {
  return (
    <>
      <div className="board-row">
        <button className="square">1</button>
        <button className="square">2</button>
        <button className="square">3</button>
      </div>
      <div className="board-row">
        <button className="square">4</button>
        <button className="square">5</button>
        <button className="square">6</button>
      </div>
      <div className="board-row">
        <button className="square">7</button>
        <button className="square">8</button>
        <button className="square">9</button>
      </div>
    </>
  );
}
```

The CSS defined in `styles.css` styles the divs with the `className` of `board-row`. Now that you've grouped your components into rows with the styled `div`s you have your tic-tac-toe board:
> `styles.css`에 정의된 CSS 스타일은 `className` 속성 값이 `board-row`인 div입니다. 이제 컴포넌트에 스타일된 `div`를 행으로 그룹화해서 tic-tac-toe 게임판을 사용할 수 있습니다:  

<img src="https://user-images.githubusercontent.com/42595869/229288252-32dbad3a-642f-4142-b125-5c3104865ecf.png" width="300" height="auto">

But you now have a problem. Your component named `Square`, really isn't a square anymore. Let's fix that by changing the named to `Board`.
> 하짐나 문제가 하나 있습니다. 컴포넌트 이름이 `Square`입니다, 이젠 더 이상 사각형이 아닙니다. `Board`로 이름을 변경하여 고칩시다.  

```tsx
export default function Board() {
  ...
}
```

At this point your code should look something like this:
> 이 시점에서 우리가 작성한 코드는 이렇게 보여야합니다:

```tsx
export default function Board() {
  return (
    <>
      <div className="board-row">
        <button className="square">1</button>
        <button className="square">2</button>
        <button className="square">3</button>
      </div>
      <div className="board-row">
        <button className="square">4</button>
        <button className="square">5</button>
        <button className="square">6</button>
      </div>
      <div className="board-row">
        <button className="square">7</button>
        <button className="square">8</button>
        <button className="square">9</button>
      </div>
    </>
  );
}
```

<img src="https://user-images.githubusercontent.com/42595869/229288463-27b442dd-7083-44b7-995f-94104b017ba5.png" width="800" height="auto">