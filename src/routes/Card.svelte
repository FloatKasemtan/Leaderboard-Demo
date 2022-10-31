<script lang="ts">
	import { slide } from 'svelte/transition';
	import randomWords from 'random-words';
	export let order: number;
	export let score: number = 0;

	const colorList = [
		'eae4e9',
		'fff1e6',
		'fde2e4',
		'fad2e1',
		'e2ece9',
		'bee1e6',
		'f0efeb',
		'dfe7fd',
		'cddafd'
	];

	function randomColor() {
		return colorList[Math.floor(Math.random() * colorList.length)];
	}

	function generate() {
		const deg = Math.floor(Math.random() * 360);

		const gradient =
			'linear-gradient(' + deg + 'deg, ' + '#' + randomColor() + ', ' + '#' + randomColor() + ')';

		return gradient;
	}

	const color = generate();
</script>

<div class="Container" in:slide style="background: {color};">
	<div class="Children">
		{order + '. ' + randomWords(5)}
		<b>{score}</b>
	</div>
</div>

<style>
	.Container {
		background-color: #f0f0f0;
		width: 100%;
		padding: 20px;
		border-radius: 15px;
	}

	.Children {
		display: flex;
		justify-content: space-between;
	}
</style>
