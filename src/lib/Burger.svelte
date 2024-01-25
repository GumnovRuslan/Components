<script>
	import { onMount } from 'svelte';

	let checkbox;
	let burger;
	let burgerLineTop;
	let burgerLineCenter;
	let burgerLineBottom;
	let time = 200;

	onMount(() => {
		checkbox = document.querySelector('.burger-checkbox');
		burger = document.querySelector('.burger');
		let lines = document.querySelectorAll('.burger__line');
		burgerLineTop = lines[0];
		burgerLineCenter = lines[1];
		burgerLineBottom = lines[2];
	});

	function burgerOpen() {
		lineTop();
		lineCenter();
		lineBottom();
	}

	function lineTop() {
		if (!checkbox.checked) {
			burgerLineTop.style.transform = 'translateY(10px)';
			setTimeout(() => {
				burgerLineTop.style.transform = 'translateY(10px) rotate(45deg)';
			}, time);
		} else {
			burgerLineTop.style.transform = 'translateY(10px) rotate(0)';
			setTimeout(() => {
				burgerLineTop.style.transform = '';
			}, time);
		}
	}
	function lineCenter() {
		if (!checkbox.checked) {
			burgerLineCenter.style.transform = 'scale(0)';
		} else {
			burgerLineCenter.style.transform = 'scale(1)';
		}
	}
	function lineBottom() {
		if (!checkbox.checked) {
			burgerLineBottom.style.transform = 'translateY(-10px)';
			setTimeout(() => {
				burgerLineBottom.style.transform = 'translateY(-10px) rotate(-45deg)';
			}, time);
		} else {
			burgerLineBottom.style.transform = 'translateY(-10px) rotate(0)';
			setTimeout(() => {
				burgerLineBottom.style.transform = '';
			}, time);
		}
	}
</script>

<input class="burger-checkbox" type="checkbox" id="falseCheckbox" />

<button class="burger" on:click={burgerOpen}>
	<label class="burger__container" for="falseCheckbox">
		<span class="burger__line burger__line-top"></span>
		<span class="burger__line burger__line-center"></span>
		<span class="burger__line burger__line-bottom"></span>
	</label>
</button>

<style>
	.burger-checkbox {
		display: none;
	}
	.burger {
		padding: 0;
		border: none;
		background: transparent;
	}
	.burger__container {
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
		gap: 6px;
		width: 50px;
		height: 50px;
		cursor: pointer;
	}
	.burger__line {
		width: 30px;
		height: 4px;
		border-radius: 5px;
		background: #000;
	}
	.burger__line-top {
		transition: all 0.2s;
	}
	.burger__line-center {
		transition: all 0.5s;
	}
	.burger__line-bottom {
		transition: all 0.2s;
	}
</style>
