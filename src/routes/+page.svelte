<script>
	import ReadMore from '../lib/ReadMore.svelte';
	import Burger from '../lib/Burger.svelte';
	import MaskNumWheel from '../lib/MaskNumWheel.svelte';
	import ClosePopup from '../lib/closePopup.svelte';
	import Slider from '../lib/slider.svelte';
	import Accordion from '../lib/Accordion.svelte';

	let cards = [
		{ id: '1', text: 'this is card 1' },
		{ id: '2', text: 'this is card 2' }
	];
</script>

<!-- <Burger /> -->
<!-- <div class="wrapper">
	{#each cards as card}
		<ReadMore id={'card-info' + card.id} />
	{/each}
</div> -->
<!-- <div class="form">
	<MaskNumWheel />
</div> -->

<!-- <ClosePopup /> -->
<!-- <Slider /> -->
<Accordion />

<style>
	.wrapper {
		display: flex;
		justify-content: center;
		gap: 20px;
	}
</style>
