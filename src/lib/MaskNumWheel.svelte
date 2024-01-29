<script>
	import { onMount } from 'svelte';

	onMount(() => {
		setWheelNumber('data-mask-num');
	});

	function setWheelNumber(attribute) {
		const inputs = document.querySelectorAll(`[${attribute}]`);
		inputs.forEach((input) =>
			input.addEventListener('wheel', (e) => {
				e.preventDefault();
				const input = e.target;
				const minNumber = input.min || 0;
				const maxNumber = input.max || 99;
				let value = input.value;
				const step = +input.step || 1;
				value = e.deltaY > 0 ? +input.value - step : +input.value + step;
				input.value = value <= minNumber ? minNumber : value >= maxNumber ? maxNumber : value;
			})
		);
	}
</script>

<input type="number" class="input-tel" data-mask-num />
