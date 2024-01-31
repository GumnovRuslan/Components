<script>
	import { onMount } from 'svelte';

	let bd = [
		{
			title: 'Title-1',
			description: 'Lorem ipsum dolor sit amet consectetur adipisicing elit. Sunt, ex! '
		},
		{
			title: 'Title-2',
			description:
				'Lorem ipsum dolor sit amet consectetur adipisicing elit. Sunt, ex! Lorem ipsum dolor sit amet consectetur adipisicing elit. Sunt, ex!'
		},
		{
			title: 'Title-3',
			description:
				'Lorem ipsum dolor sit amet consectetur adipisicing elit. Sunt, ex! Lorem ipsum dolor sit amet consectetur adipisicing elit. Sunt, ex! Lorem ipsum dolor sit amet consectetur adipisicing elit. Sunt, ex!'
		},
		{
			title: 'Title-4',
			description:
				'Lorem ipsum dolor sit amet consectetur adipisicing elit. Sunt, ex! Lorem ipsum dolor sit amet consectetur adipisicing elit. Sunt, ex! Lorem ipsum dolor sit amet consectetur adipisicing elit. Sunt, ex! Lorem ipsum dolor sit amet consectetur adipisicing elit. Sunt, ex!'
		}
	];

	let accordionItems;

	onMount(() => {
		accordionItems = document.querySelectorAll('.accordion__header');
		accordionItems.forEach((item) => item.addEventListener('click', accordion));
	});

	function accordion(e) {
		const accordion = e.target.closest('.accordion');
		const items = accordion.querySelectorAll('.accordion__item');
		const item = e.target.closest('.accordion__item');

		function close(el) {
			const line = el.querySelectorAll('.accordion__marker-line')[1];
			const info = el.querySelector('.accordion__info');
			info.style.height = `${0}px`;
			el.dataset.open = 0;
			line.style.transform = 'rotate(90deg)';
		}
		function open(el) {
			const line = el.querySelectorAll('.accordion__marker-line')[1];
			const info = el.querySelector('.accordion__info');
			info.style.height = `${info.scrollHeight}px`;
			el.dataset.open = 1;
			line.style.transform = 'rotate(0deg)';
		}

		function onlyOneIsOpen() {
			if (!+item.dataset.open)
				items.forEach((el) => (el != item ? +el.dataset.open && close(el) : open(el)));
			else close(item);
		}
		function allOpen() {
			!+item.dataset.open ? open(item) : close(item);
		}

		onlyOneIsOpen();
		// allOpen();
	}
</script>

<div class="accordion">
	{#each bd as item}
		<div class="accordion__item" data-open="0">
			<div type="button" class="accordion__header">
				<p class="accordion__title">{item.title}</p>
				<div class="accordion__marker">
					<div class="accordion__marker-line"></div>
					<div class="accordion__marker-line"></div>
				</div>
			</div>
			<div class="accordion__info">
				<p class="accordion__text">{item.description}</p>
			</div>
		</div>
	{/each}
</div>

<style>
	.accordion {
		width: 450px;
	}
	.accordion__item {
		background: #3838a9;
		border-left: 1px solid #000;
		border-right: 1px solid #000;
		border-bottom: 1px solid #000;
	}
	.accordion__item:first-child {
		border-top: 1px solid #000;
	}
	.accordion__header {
		display: flex;
		justify-content: space-between;
		align-items: center;
		gap: 10px;
		border: none;
		padding: 10px 20px;
		cursor: pointer;
		background: #2e2e8a;
	}
	.accordion__title {
		margin: 0;
		font-size: 20px;
		font-weight: 700;
		letter-spacing: 1px;
		color: #f5f5f5;
	}
	.accordion__info {
		height: 0;
		padding: 0px 20px;
		overflow: hidden;
		transition: height 0.5s;
	}
	.accordion__text {
		margin: 0;
		padding: 10px 0;
		font-size: 18px;
		color: #f5f5f5;
	}
	.accordion__marker {
		position: relative;
		right: 0;
		width: 25px;
		height: 25px;
	}
	.accordion__marker-line {
		position: absolute;
		top: 50%;
		left: 0;
		transform: translateY(-50%);
		width: 100%;
		height: 3px;
		background: #f5f5f5;
		transition: all 0.5s;
	}
	.accordion__marker-line:nth-child(1) {
		transform: rotate(0);
	}
	.accordion__marker-line:nth-child(2) {
		transform: rotate(90deg) scale(1);
	}
</style>
