<script>
	import { onMount } from 'svelte';

	let buttons; //only elements with data-tooltip
	let tooltipElem;
	onMount(() => {
		buttons = document.querySelectorAll('button[data-tooltip]');
		buttons.forEach((button) => setTooltip(button));
	});

	function setTooltip(button) {
		button.addEventListener('mouseover', openTooltip);
		button.addEventListener('mouseout', closeTooltip);

		function openTooltip() {
			let tooltipText = button.dataset.tooltip;
			if (!tooltipText) return;
			else createTooltip(tooltipText);

			const coords = button.getBoundingClientRect();
			let left = coords.left + (button.offsetWidth - tooltipElem.offsetWidth) / 2;
			if (left < 0) left = 0;

			let top = coords.top - tooltipElem.offsetHeight - 5;
			if (top < 0) top = coords.top + button.offsetHeight + 5;

			tooltipElem.style.left = left + 'px';
			tooltipElem.style.top = top + 'px';
		}

		function closeTooltip() {
			if (tooltipElem) tooltipElem.remove();
		}

		function createTooltip(text) {
			tooltipElem = document.createElement('div');
			tooltipElem.className = 'tooltip';
			tooltipElem.innerHTML = text;
			button.append(tooltipElem);
			// tooltipElem.style.position = 'fixed';
			tooltipElem.style.cssText = `
					position: fixed;
					padding: 15px;
					border: 2px solid #b9b9b9;
					border-radius: 4px;
					text-align: center;
					background: #f5f5f5;
				`;
		}
	}
	// $: if (tooltipElem) tooltipElem.classList.add('tooltip');
</script>

<p>
	Lorem ipsum, dolor sit amet consectetur adipisicing elit. Iusto vitae ratione voluptate laudantium
	ea reprehenderit aspernatur! Repellat et quod itaque facere alias, veritatis fuga officia optio,
	tempore rem sint. Magni.
</p>
<p>
	Lorem ipsum, dolor sit amet consectetur adipisicing elit. Iusto vitae ratione voluptate laudantium
	ea reprehenderit aspernatur! Repellat et quod itaque facere alias, veritatis fuga officia optio,
	tempore rem sint. Magni.
</p>
<p>
	Lorem ipsum, dolor sit amet consectetur adipisicing elit. Iusto vitae ratione voluptate laudantium
	ea reprehenderit aspernatur! Repellat et quod itaque facere alias, veritatis fuga officia optio,
	tempore rem sint. Magni.
</p>

<button class="btn" data-tooltip="длинный текст с подсказкой">Кнопка 1</button>
<button class="btn" data-tooltip="Подсказка с <br> HTML тегами">Кнопка 2</button>
<button class="btn" data-tooltip="0">Кнопка 3</button>

<style>
	.btn {
		padding: 5px 20px;
		background: #d9cffa;
		border: 1px solid #000;
		border-radius: 4px;
	}
	.tooltip {
		position: fixed;
		padding: 15px;
		border: 2px solid #b9b9b9;
		border-radius: 4px;
		text-align: center;
		background: #f5f5f5;
	}
</style>
