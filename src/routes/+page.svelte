<script>
	import ReadMore from '../lib/ReadMore.svelte';
	import Burger from '../lib/Burger.svelte';

	let cards = [
		{ id: '1', text: 'this is card 1' },
		{ id: '2', text: 'this is card 2' }
	];
</script>

<div class="wrapper">
	{#each cards as card}
		<ReadMore id={'card-info' + card.id} />
	{/each}
</div>

<style>
	.wrapper {
		display: flex;
		justify-content: center;
		gap: 20px;
	}
</style>
