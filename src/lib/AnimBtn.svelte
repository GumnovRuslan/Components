<script>
	import { onMount } from 'svelte';

	onMount(() => {});

	function btnMove(e) {
		const btn = e.target;
		let x = e.pageX - btn.offsetLeft;
		let y = e.pageY - btn.offsetTop;

		btn.style.setProperty('--x', x + 'px');
		btn.style.setProperty('--y', y + 'px');
	}
</script>

<div class="container">
	<button class="btn" on:mousemove={btnMove}> </button>
</div>

<style>
	.container {
		height: 500px;
		display: flex;
		align-items: center;
		justify-content: center;
	}
	.btn {
		position: relative;
		width: 300px;
		height: 100px;
		border-radius: 5px;
		border: none;
		background: #292929;
		overflow: hidden;
		cursor: pointer;
	}

	.btn::after {
		content: '';
		position: absolute;
		top: var(--y);
		left: var(--x);
		width: 0px;
		height: 0px;
		border-radius: 50%;
		background: #4070f4;
		transition:
			top 0.1s,
			left 0.1s,
			width 0.5s,
			height 0.5s;
		transform: translate(-50%, -50%);
	}
	.btn:hover::after {
		width: 200px;
		height: 200px;
	}
	.btn:before {
		content: 'Hover me!';
		position: absolute;
		z-index: 2;
		top: 50%;
		left: 50%;
		transform: translate(-50%, -50%);
		color: #f5f5f5;
		font-size: 20px;
	}
</style>
