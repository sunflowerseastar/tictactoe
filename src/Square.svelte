<script>
export let addPiece;
export let sq;
export let x;
export let y;
</script>

<style>
.square {
	position: relative;
	padding-bottom: 100%;
	cursor: pointer;
}
.square.contains-x {
	background: black;
}
.square.contains-o {
	background: repeating-linear-gradient(-45deg, #000, #000 12px, #fff 0, #fff 20px);
}
.square-inner {
	position: absolute;
	top: 0;
	left: 0;
}
</style>

<span class="square x{x+1} y{y+1} contains-{sq}" on:click={() => {!sq.length && addPiece(sq,x,y)}}></span>
