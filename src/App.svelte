<script>
import Board from './Board.svelte';

let currentTurn = 'x';
let currentWinner = '';
let canRestart = false;

let board = [['', '', ''], ['', '', ''], ['', '', '']];

const restart = () => {
  board = [['', '', ''], ['', '', ''], ['', '', '']];
  currentTurn = 'x';
  currentWinner = '';
  canRestart = false;
};

const winnerExists = board => {
  const ttt1 = [board[0][0], board[0][1], board[0][2]];
  const ttt2 = [board[1][0], board[1][1], board[1][2]];
  const ttt3 = [board[2][0], board[2][1], board[2][2]];
  const ttt4 = [board[0][0], board[1][0], board[2][0]];
  const ttt5 = [board[0][1], board[1][1], board[2][1]];
  const ttt6 = [board[0][2], board[1][2], board[2][2]];
  const ttt7 = [board[0][0], board[1][1], board[2][2]];
  const ttt8 = [board[0][2], board[1][1], board[2][0]];

  const allEqual = arr => arr.every(x => x.length && x === arr[0]);
  const ttts = [ttt1, ttt2, ttt3, ttt4, ttt5, ttt6, ttt7, ttt8].map(allEqual);
  return ttts.some(z => z === true);
};

const addPiece = (sq, x, y) => {
  board[y][x] = currentTurn;

  if (winnerExists(board)) {
    currentWinner = currentTurn;
    canRestart;
    setTimeout(() => {
      canRestart = true;
    }, 0);
  } else {
    currentTurn = currentTurn === 'x' ? 'o' : 'x';
    canRestart = false;
  }
};
</script>

<style>
:global(body) {
  padding: 0;
  color: white;
  background: black;
  text-align: center;
}
.container {
  height: 100vh;
}
.container.current-x {
  background: black;
}
.container.current-o {
  background: repeating-linear-gradient(-45deg, #000, #000 12px, #fff 0, #fff 20px);
}
.inner {
  height: 100vh;
  display: flex;
  flex-direction: column;
  justify-content: flex-end;
  box-sizing: border-box;
}
.click-overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100vw;
  height: 100vh;
  pointer-events: none;
}
.click-overlay.active {
  pointer-events: auto;
}
</style>

<div class:active={canRestart} class="click-overlay" on:click={() => canRestart && restart()}></div>
<div class="container current-{currentTurn}">
	<div class="inner">
		<Board board={board} addPiece={addPiece} />
	</div>
</div>
