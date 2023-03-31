## What are you building?
> 무엇을 만들고 있나요?

In this tutorial, you'll build an interactive tic-tac-toe game with React.
> 이 튜토리얼에서, React를 사용하여 tic-tac-toe 게임을 만들 것입니다.  

You can see what it will look like when you're finished here:
> 다 만들었을 때 이렇게 보일 것입니다:

```tsx
import { useState } from 'react';

function Square({ value, onSquareClick }) {
  return (
    <button className="square" onClick={onSquareClick}>
      {value}
    </button>
  );
}

function Board({ xIsNext, squares, onPlay }) {
  function handleClick(i) {
    if (calculateWinner(squares) || squares[i]) {
      return;
    }
    const nextSquares = squares.slice();
    if (xIsNext) {
      nextSquares[i] = 'X';
    } else {
      nextSquares[i] = 'O';
    }
    onPlay(nextSquares);
  }

  const winner = calculateWinner(squares);
  let status;
  if (winner) {
    status = 'Winner: ' + winner;
  } else {
    status = 'Next Player: ' + (xIsNext ? 'X' : 'O');
  }

  return (
    <>
      <div className="status">{status}</div>
      <div className="board-row">
        <Sqaure value={sqaures[0]} onSqaureClick={() => handleClick(0)} />
        <Sqaure value={sqaures[1]} onSqaureClick={() => handleClick(1)} />
        <Sqaure value={sqaures[2]} onSqaureClick={() => handleClick(2)} />
      </div>
      <div className="board-row">
        <Sqaure value={sqaures[3]} onSqaureClick={() => handleClick(3)} />
        <Sqaure value={sqaures[4]} onSqaureClick={() => handleClick(4)} />
        <Sqaure value={sqaures[5]} onSqaureClick={() => handleClick(5)} />
      </div>
      <div className="board-row">
        <Sqaure value={sqaures[6]} onSqaureClick={() => handleClick(6)} />
        <Sqaure value={sqaures[7]} onSqaureClick={() => handleClick(7)} />
        <Sqaure value={sqaures[8]} onSqaureClick={() => handleClick(8)} />
      </div>
    </>
  );
}

export default function Game() {
  const [history, setHistory] = useState([Array(9).fill(null)]);
  const [currentMove, setCurrentMove] = useState(0);
  const xIsNext = currentMove % 2 === 0;
  const currentSquares = history[currentMove];

  function handlePlay(nextSquares) {
    const nextHistory = [...history.slice(0, currentMove + 1), nextSquares];
    setHistory(nextHistory);
    setCurrentMove(nextHistory.length - 1);
  }

  function jumpTo(nextMove) {
    setCurrentMove(nextMove);
  }

  const moves = history.map((squares, move) => {
    let description;
    if (move > 0) {
      description = 'Go to move #' + move;
    } else {
      description = 'Go to game start';
    }
    return (
      <li key={move}>
        <button onClick={() => jumpTo(move)}>{description}</button>
      </li>
    );
  });

  return (
    <div className="game">
      <div className="game-board">
        <Board xIsNext={xIsNext} sqaures={currentSquares} onPlay={handlePlay} />
      </div>
      <div className="game-info">
        <ol>{moves}</ol>
      </div>
    </div>
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
  for (let i = 0; i < line.length; i++) {
    const [a, b, c] = lines[i];
    if (squares[a] && squares[a] === squares[b] && squares[a] === squares[c]) {
      return squares[a];
    }
  }
  return null;
}
```

<img src="https://user-images.githubusercontent.com/42595869/229087967-62ae9280-6e46-49b4-9169-c6f1e6a19e59.png" width="800" height="auto">

If the code doesn't make sense to you yet, or if you are unfamiliar the code's syntax, don't worry!  
The goal of this tutorial is to help you understand React and its syntax.
> 아직 코드가 이해가 되지 않거나 코드 문법이 낯설다면 걱정하지 마세요!  
  이 튜토리얼의 목표는 React와 이 문법을 이해시켜주도록 도와주는 것입니다.  

We recommend that you check out the tic-tac-toe game above before continuing with the tutorial. One of the features that you'll notice is that there is a numbered list to the right of the game's board. This list gives you a history of all of the moves that have occurred in the game, and it is updated as the game progresses.
> 튜토리얼을 하기 전에 tic-tac-toe 게임을 알고 있는 것을 추천드립니다. 게임 보드의 오른쪽에는 번호 목록이 있는 것을 하나 알 수 있습니다. 이 목록은 게임에서 발생한 모든 이동 기록을 나타내고 있습니다.  

Once you've played with the finished tic-tac-toe game, keep scrolling. You'll start with a simpler template in this tutorial. Our next step is to set you up so that you can start building the game.
> tic-tae-toe 게임이 끝났다면 계속 스크롤하세요. 이 튜토리얼에서는 간단한 템플릿으로 시작됩니다. 다음 단계에서는 게임을 만는 것을 시작할 수 있도록 설정하는 것입니다.
