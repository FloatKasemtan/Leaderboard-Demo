<script lang="ts">
	import { slide } from 'svelte/transition';
	import randomWords from 'random-words';
	export let order: number;

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
</script>

<div class="Container" in:slide style="background: {generate()};">
	<div>{order + '. ' + randomWords(5)}</div>
</div>

<style>
	.Container {
		background-color: #f0f0f0;
		width: 100%;
		padding: 20px;
		border-radius: 15px;
	}
</style>
