<script>
	import Tile from '$lib/Tile.svelte';
	import svelte from '$assets/svelte.png';
	import css from '$assets/css.png';
	import html from '$assets/html.png';
	import ts from '$assets/typescript.png';
	import angular from '$assets/angular.png';
	import js from '$assets/js.png';
	import node from '$assets/node.png';
	import react from '$assets/react.png';

	let tiles = [
		{ src: svelte, faceDown: true, solved: false },
		{ src: css, faceDown: true, solved: false },
		{ src: svelte, faceDown: true, solved: false },
		{ src: html, faceDown: true, solved: false },
		{ src: js, faceDown: true, solved: false },
		{ src: css, faceDown: true, solved: false },
		{ src: react, faceDown: true, solved: false },
		{ src: angular, faceDown: true, solved: false },
		{ src: html, faceDown: true, solved: false },
		{ src: js, faceDown: true, solved: false },
		{ src: angular, faceDown: true, solved: false },
		{ src: ts, faceDown: true, solved: false },
		{ src: node, faceDown: true, solved: false },
		{ src: react, faceDown: true, solved: false },
		{ src: ts, faceDown: true, solved: false },
		{ src: node, faceDown: true, solved: false },
	].sort(() => 0.5 - Math.random())

	let selected = 0;

	$: {
		if (selected === 2) {
			let faceUp = tiles.filter((t) => !t.faceDown);
			if (faceUp.length === 2 && faceUp[0].src === faceUp[1].src) {
				tiles = tiles.map((t) => ({ ...t, solved: t.solved || t.src === faceUp[0].src }));
			}
			setTimeout(() => {
				tiles = tiles.map((t) => ({ ...t, faceDown: true }));
				selected = 0;
			}, 1000);
		}
		if (selected > 2) {
			tiles = tiles.map((t) => ({ ...t, faceDown: true }));
			selected = 0;
		}
	}
	$: {
		if (tiles.filter((t) => t.solved).length === tiles.length) {
			setTimeout(() => {
				tiles = tiles.sort(() => 0.5 - Math.random()).map((t) => ({ ...t, solved: false, faceDown: true }));
			}, 1000);
		}
	}
</script>

<main>
	{#each tiles as { src, faceDown, solved }}
		<div>
			<Tile on:tileClicked={() => selected++} bind:faceDown {src} bind:solved />
		</div>
	{/each}
</main>

<style>
	main {
		text-align: center;
		padding: 1em;
		margin: 0 auto;
		width: 90vh;
		height: 90vh;
		display: grid;
		grid-template-columns: repeat(4, 1fr);
		gap: 5px;
	}
	div {
		width: calc(90vh / 4);
	}
</style>
