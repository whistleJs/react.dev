## Declaring a winner
> 승자 선언하기

Now that the players can take turns, you'll want to show when the game is won and there are no more turns to make. To do this you'll add a helper function called `calculateWinner` that takes an array of 9 squares, checks for a winner and returns `'X'`, `'O'`, or `null` as appropriate.
> 이제 플레이어들이 교대로 할 수 있고, 게임에서 이기고 더 이상 할 차례가 없는 것을 보여주는 것을 원합니다. 이를 위해 9개 사각형의 배열을 가지고 승자를 `'X'`, `'O'` 또는 `null`을 반환하는 `calculateWinner`라는 함수를 추가합니다. 

Don't worry too much about the `calculateWinner` function; it's not specific to React:
`calculateWinner` 함수에 대해 너무 걱정하지 마세요; React에서 구체적이지 않습니다:  

```tsx
export default function Board() {
  // ...
}

function calculateWinner(squares) {
  const lines = [
    [0, 1, 2],
    [3, 4, 5],
    [6, 7, 8],
    [0, 3, 6],
    [1, 4, 7],
    [2, 5, 8],
    [0, 4, 8],
    [2, 4, 6]
  ];
  for (let i = 0; i < lines.length; i++) {
    const [a, b, c] = lines[i];
    if (squares[a] && squares[a] === squares[b] && squares[a] === squares[c]) {
      return squares[a];
    }
  }
  return null;
}
```

You will call `calculateWinner(squares)` in the `Board` component's `handleClick` function to check if a player has won. You can perform this check at the same time you check if a user has clicked a square that already has a `X` or and `O`. We'd like to return early in both cases:
> `Board` 컴포넌트의 `handleClick` 함수에서 플레이어가 이겼는지 확인하도록 `calculateWinner(squares)`를 호출하면 될 것입니다. 사용자가 이미 `X` 또는 `O`를 가지고 있는 사각형을 클릭했을 때와 동시에 이 검사를 확인할 수 있습니다. 두 경우에 대해 일찍 반환하면 됩니다:  

```tsx
function handleClick(i) {
  if (squares[i] || calculateWinner(squares)) {
    return;
  }
  const nextSquares = squares.slice();
  // ...
}
```

To let the players know when the game is over, you can display text such as "Winner: X" or "Winner: O". To do that you'll add a `status` section to the `Board` component. The status will display the winner if the game is over and if the game is ongoing you'll display which player's turn is next:
> 게임이 끝날 때 플레이어가 알 수 있도록 하려면 "Winner: X" 또는 "Winner: O"를 표시하면 됩니다. `Board` 컴포넌트에 `status` 섹션을 추가하여 해봅시다. status는 게임이 끝났을 때 승자를 표시하거나 게임이 진행 중일 때 다음 플레이어 차례를 표시합니다:  

```tsx
export default function Board() {
  // ...
  const winner = calculateWinner(squares);
  let status;
  if (winner) {
    status = "Winner: " + winner;
  } else {
    status = "Next Player: " + (xIsNext ? "X" : "O");
  }

  return (
    <>
      <div className="status">{status}</div>
      <div className="board-row">
        // ...
  );
}
```

Congraulations! You now have a working tic-tac-toe game. And you've just learned the basics of React too. So you are the real winner here. Here is what the code should look like:
> 축하합니다! 이제 tic-tac-toc 게임이 동작합니다. 그리고 React의 기초도 배웠습니다. 진짜 승자는 당신입니다. 여기에 코드가 이렇게 보일 겁니다:  

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
    if (squares[i] || calculateWinner(squares)) {
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

  const winner = calculateWinner(squares);
  let status;
  if (winner) {
    status = 'Winner: ' + winner;
  } else {
    status = 'Next player: ' + (xIsNext ? 'X' : 'O');
  }

  return (
    <>
      <div className="status">{status}</div>
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

function calculateWinner(squares) {
  const lines = [
    [0, 1, 2],
    [3, 4, 5],
    [6, 7, 8],
    [0, 3, 6],
    [1, 4, 7],
    [2, 5, 8],
    [0, 4, 8],
    [2, 4, 6]
  ];
  for (let i = 0; i < lines.length; i++) {
    const [a, b, c] = lines[i];
    if (squares[a] && squares[a] === squares[b] && squares[a] === squares[c]) {
      return squares[a];
    }
  }
  return null;
}
```

<img src="https://user-images.githubusercontent.com/42595869/230873593-34a0b72e-1cd6-484c-b39e-003b1068b45d.png" width="800" height="auto">