<script>
let currentTurn = 'x';
let winner = '';

let board = [['', '', ''], ['', '', ''], ['', '', '']];

const restart = () => {
  board = [['', '', ''], ['', '', ''], ['', '', '']];
  currentTurn = '';
  winner = '';
};

const winnerExists = board => {
  console.log('winnerExists', board);

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
  console.log('addPiece', sq, x, y);

  board[y][x] = currentTurn;

  const we = winnerExists(board);
  // console.log('we', we);

  if (we) {
    console.log('yes winner', currentTurn);
    winner = currentTurn;
  } else {
    console.log('no winner');
    currentTurn = currentTurn === 'x' ? 'o' : 'x';
  }
};
</script>

<main>
	{#each board as row, y}

{#each row as sq, x}
	<span on:click={() => {!sq.length && addPiece(sq,x,y)}}>{sq}</span>
	{/each}
<br/>
	{/each}
<br/>
<h6>{currentTurn}</h6>
	 {#if winner.length > 0}
	 <h1>Winner: {currentTurn}</h1>
	 <a on:click={restart}>restart</a>
	 {/if}
</main>

<style>
	 span {
		 display: inline-block;
		 width: 20px;
		 height: 20px;
		 border: 1px solid #eee;
		 cursor: pointer;
	 }
</style>
