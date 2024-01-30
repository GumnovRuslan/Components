<script>
	import { onMount } from 'svelte';

	let popup;

	onMount(() => {
		popup = document.querySelector('.popup');
		popup.addEventListener('click', closeDialog);
	});

	function closeDialog(e) {
		const dialogSize = popup.getBoundingClientRect();
		if (
			e.clientX < dialogSize.left ||
			e.clientX > dialogSize.right ||
			e.clientY < dialogSize.top ||
			e.clientY > dialogSize.bottom
		)
			popup.close();
	}
</script>

<dialog class="popup">
	<p class="popup__text">
		Lorem ipsum dolor sit amet, consectetur adipisicing elit. Modi delectus cupiditate quae, eius
		deserunt soluta quod dolorem dolore in ipsam laboriosam vel, autem qui odio odit! Nihil
		obcaecati ducimus esse aperiam in, aspernatur quis placeat ipsum cumque deleniti, temporibus
		reprehenderit laudantium sint tempora, dolore nam. In earum velit ipsam officia modi sit a odit
		repellendus quo quae beatae accusamus eius maiores necessitatibus porro ipsa, delectus voluptate
		ullam aliquid molestias voluptatem? Deserunt sint laudantium non qui nihil facilis nostrum nemo,
		fuga ut unde impedit reprehenderit magni odit soluta similique esse ipsam quis labore corrupti
		voluptatum fugiat! Minima quod blanditiis fuga quos.
	</p>
</dialog>

<button class="btn-popup" on:click={() => popup.showModal()}>Открыть окно</button>

<style>
	.popup {
		max-width: 80vw;
	}
</style>
