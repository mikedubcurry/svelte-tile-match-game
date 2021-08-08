<script>
	import { createEventDispatcher } from 'svelte';

	export let faceDown = false;
	export let src;
	export let solved = false;

	const dispatch = createEventDispatcher();
</script>

<div
	on:click={() => {
		if (!solved || faceDown) {
			faceDown = false;
			dispatch('tileClicked');
		}
	}}
	class:faceDown
	class:solved
	class="tile"
>
	<img {src} alt="a tile, what could it be?" />
</div>

<style>
	.tile {
		width: 100%;
		height: 100%;
		background-color: rebeccapurple;
		transform-style: preserve-3d;
		transform: rotateY(0deg);
		transition: transform 0.3s ease, background-color 0.2s ease;
		position: relative;
		display: flex;
		justify-content: center;
		align-items: center;
	}
	.tile::after {
		width: 100%;
		height: 100%;
		content: '';
		background-color: #ddd;
		position: absolute;
		top: 0;
		left: 0;
		transform: rotateY(180deg);
		transition: transform 0.3s ease, background-color 0.2s ease;
		transform-style: preserve-3d;
		backface-visibility: hidden;
		-webkit-backface-visibility: hidden;
	}

	.tile.faceDown {
		transform: rotateY(180deg);
	}
	.tile.faceDown::before {
		transform: rotateY(0deg);
	}
	.tile.tile.solved {
		transform: rotateY(0deg);
		background-color: gold;
	}
	.tile:hover::after {
		background-color: #eee;
	}

	img {
		width: 90%;
	}
</style>
