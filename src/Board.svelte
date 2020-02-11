<script>
import Square from './Square.svelte';

export let addPiece;
export let board;
</script>

<style>
.board-container {
  flex: 1;
  display: flex;
  flex-direction: column;
  justify-content: center;
}
.board {
  position: relative;
  align-self: center;
  display: grid;
  width: 100%;
  max-width: 55vh;
  margin: 0 auto;
  grid-template-columns: repeat(3, 1fr);
  background: white;
}
@media (min-width: 480px) {
  .board {
    width: 80%;
  }
}
@media (min-width: 768px) {
  .board {
    width: 90%;
    max-width: 72vh;
  }
}
</style>

<div class="board-container">
	<div class="board">
		{#each board as row, y}
			{#each row as sq, x}
        <Square x={x} y={y} sq={sq} addPiece={addPiece} />
			{/each}
		{/each}
	</div>
</div>
