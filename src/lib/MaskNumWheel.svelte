<script>
	import { onMount } from 'svelte';

	onMount(() => {
		setWheelNumber('data-mask-num');
	});

	function setWheelNumber(attribute) {
		const inputs = document.querySelectorAll(`[${attribute}]`);
		inputs.forEach((input) => {
			input.addEventListener('wheel', wheelNumber);
			input.addEventListener('input', limitationNumber);
		});

		function wheelNumber(e) {
			e.preventDefault();
			const input = e.target;
			const minNumber = input.min || 0;
			const maxNumber = input.max || 99;
			let value = input.value;
			const step = +input.step || 1;
			value = e.deltaY > 0 ? +input.value - step : +input.value + step;
			input.value = value <= minNumber ? minNumber : value >= maxNumber ? maxNumber : value;
		}

		function limitationNumber(e) {
			let input = e.target;
			let inputValue = input.value;
			let maxValue = input.max || 100;
			let minValue = input.min || 0;

			if (inputValue == '') return (e.target.value = '');
			if (inputValue.length > 1 && inputValue[0] == 0) inputValue = inputValue.slice(1);
			if (+inputValue > +maxValue) inputValue = maxValue;
			else if (+inputValue < +minValue) inputValue = minValue;
			e.target.value = inputValue;
		}
	}
</script>

<input type="number" class="input-tel" data-mask-num />
