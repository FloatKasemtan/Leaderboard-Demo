<script lang="ts">
	import Card from './Card.svelte';
	import { flip } from 'svelte/animate';
	import type { CardType } from 'src/types/types';
	const soundSrc = 'src/lib/reorder_sound.wav';

	let freq: number = 250;
	let time: number = 5000;
	let disable: boolean = false;
	let list: Array<CardType> = [
		{ text: '1', order: 1 },
		{ text: '2', order: 2 },
		{ text: '3', order: 3 },
		{ text: '4', order: 4 },
		{ text: '5', order: 5 }
	];

	function addCard() {
		list = [
			...list,
			{
				text: `${list.length + 1}`,
				order: list.length + 1
			}
		];
	}

	function reorderAscend() {
		list = list.sort((a, b) => {
			if (a.order > b.order) {
				return 1;
			} else if (b.order > a.order) {
				return -1;
			} else {
				return 0;
			}
		});
	}

	function reorderDecend() {
		list = list.sort((a, b) => {
			if (a.order > b.order) {
				return -1;
			} else if (b.order > a.order) {
				return 1;
			} else {
				return 0;
			}
		});
	}

	function reorderRandom() {
		const audio = new Audio(soundSrc);
		disable = true;
		var interval = setInterval(() => {
			list = list.sort((a, b) => {
				return Math.random() - 0.5;
			});
			//@ts-ignore
			audio.cloneNode(true).play();
		}, freq);

		setTimeout(() => {
			clearInterval(interval);
			disable = false;
		}, time);
	}
</script>

<svelte:head>
	<title>Home</title>
	<meta name="description" content="Svelte demo app" />
</svelte:head>

<section>
	<h1>Just me try to play with Svelte</h1>

	<div class="button-container">
		<button disabled={disable} on:click={reorderAscend}>Ascend</button>
		<button disabled={disable} on:click={reorderDecend}>Decend</button>
		<button disabled={disable} on:click={addCard}>add</button>
	</div>
	<div class="button-container">
		<button disabled={disable} on:click={reorderRandom}>Random</button>
		<input disabled={disable} bind:value={freq} placeholder="freq" type="number" />
		<input disabled={disable} bind:value={time} placeholder="time" type="number" />
	</div>
	<div class="Card-container">
		{#each list as item (item.order)}
			<div
				animate:flip={{
					duration: (d) => {
						return 50 * Math.sqrt(d);
					}
				}}
			>
				<Card order={item.order} />
			</div>
		{/each}
	</div>
</section>

<style>
	section {
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		flex: 0.6;
	}

	h1 {
		width: 100%;
	}

	.Card-container {
		gap: 12px;
		display: flex;
		flex-direction: column;
		margin: auto;
		width: 50vw;
	}

	.button-container {
		display: flex;
		gap: 20px;
		margin: 10px;
	}

	button {
		transition: 1s cubic-bezier(0.075, 0.82, 0.165, 1);
		padding: 20px;
		background-color: linear-gradient(90deg, rgba(195, 155, 218, 1) 0%, rgba(193, 97, 164, 1) 100%);
		border-radius: 15px;
		border: none;
	}

	input {
		transition: 1s cubic-bezier(0.075, 0.82, 0.165, 1);
		padding: 20px;
		border-radius: 15px;
		border: none;
	}
</style>
