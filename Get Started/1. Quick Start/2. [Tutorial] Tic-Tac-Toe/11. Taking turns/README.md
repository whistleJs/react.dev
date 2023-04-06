## Tacking turns
> 턴 바꾸기

It's now time to fix a major defect in this tic-tac-toe game: the "O"s cannot be marked on the board.
> 이제 tic-tac-toe 게임의 주요 이슈를 수정할 차례입니다: 게임판에서 "O"를 채울 수 없습니다.

You'll set the first move to be "X" by default. Let's keep track of this by adding another piece of state to the Board component:
> 기본적으로 첫번째 이동은 "X"로 설정되어 있습니다. Board 컴포넌트의 또 다른 state를 추가하여 이 문제를 추적해보겠습니다:  

```tsx
function Board() {
  const [xIsNext, setXIsNext] = useState(true);
  const [squares, setSquares] = useState(Array(9).fill(null));

  // ...
}
```

Each time a player moves, `xIsNext` (a boolean) will be flipped to determine which player goes next and the game's state will be saved. You'll update th `Board`'s `handleClick` function to flip the value of `xIsNext`:
> 플레이어가 이동할 때마다, `xIsNext` (boolean형) 이 반대로 되어 다음 플레이어를 결정하고 게임의 상태가 저장됩니다. `Board`의 `handleClick` 함수에서 `xIsNext` 값을 반대로 변경해줍니다:  

```tsx
export default function Board() {
  const [xIsNext, setXIsNext] = useState(true);
  const [squares, setSquares] = useState(Array(9).fill(null));

  function handleClick(i) {
    const nextSquares = squares.slice();
    if (xIsNext) {
      nextSquares[i] = "X";
    } else {
      nextSquares[i] = "O";
    }
    setSquares(nextSquares);
    setXIsNext(!xIsNext);
  }

  return (
    // ...
  );
}
```

Now, as you click on different squares, they will alternate between `X` and `O`, as they should!
> 이제 다른 사각형들을 클릭할 때, `X`와 `O`로 번갈아가며 채워집니다!

But wait, there's a problem. Try clicking on the same square multiple times:
> 하지만 문제가 있습니다. 같은 사각형을 여러번 클릭해보세요:

<img src="https://react.dev/images/tutorial/tictac-adding-x-s.gif" width="300" height="auto">

The `X` is overwritten by an `O`! While this would add a very interesting twist to the game, we're going to stick to the original rules for now.
> `X`가 `O`로 덮여쓰여집니다! 이 이슈는 게임에 매우 흥미로운 반전을 추가할 수 있지만, 원래의 규칙을 따라가겠습니다.

When you mark a square with a `X` or an `O` you aren't first checking to see if the square already has a `X` or `O` value. You can fix this by _returning early_. You'll check to see if the square already has a `X` or an `O`.
> 사각형에 `X` 또는 `O`를 표시할 때 해당 사각형에 `X` 또는 `O`가 있는지 확인하고 있지 않습니다. *먼저 return*하는 것으로 고칠 수 있습니다. 사각형이 이미 `X` 또는 `O`로 채워져 있는지 확인해봐야 합니다.

If the square is already filled, you will `return` in the `handleClick` function early - before it tries to update the board state.
사각형이 이미 채워져있다면, `handleClick` 함수에서 먼저 `return`할 수 있습니다 - board state를 변경하기 전

```tsx
function handleClick(i) {
  if (squares[i]) {
    return;
  }
  const nextSquares = squares.slice();
  // ...
}
```

Now you can only add `X`'s or `O`'s to empty squares! Here is what your code should look like at this point:
> 이제 비어있는 사각형에만 `X` 또는 `O`를 채울 수 있습니다! 이 시점에서 코드는 이렇게 보일 겁니다:

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
  const [xIsNext, setXIsNext] = useState(true);
  const [squares, setSquares] = useState(Array(9).fill(null));

  function handleClick(i) {
    if (squares[i]) {
      return;
    }
    const nextSquares = squares.slice();
    if (xIsNext) {
      nextSquares[i] = 'X';
    } else {
      nextSquares[i] = 'O';
    }
    setSquares(nextSquares);
    setXIsNext(!xIsNext);
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

<img src="https://user-images.githubusercontent.com/42595869/230280182-1309cf1a-514a-422e-b943-bc682c181e3f.png" width="800" height="auto">