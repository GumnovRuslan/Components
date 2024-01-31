<script>
	import { onMount } from 'svelte';

	let tooltipElem;

	onMount(() => {
		document.onmouseover = function (e) {
			let target = e.target;
			let tooltipHtml = target.dataset.tooltip;
			if (!tooltipHtml) return;
			tooltipElem = document.createElement('div');
			tooltipElem.className = 'tooltip';
			tooltipElem.innerHTML = tooltipHtml;
			document.body.append(tooltipElem);
			tooltipElem.style.cssText = `
                position: fixed;
                padding: 15px;
                border: 2px solid #b9b9b9;
                border-radius: 4px;
                text-align: center;
                background: #f5f5f5;
            `;

			let coords = target.getBoundingClientRect();
			let left = coords.left + (target.offsetWidth - tooltipElem.offsetWidth) / 2;
			if (left < 0) left = 0;

			let top = coords.top - tooltipElem.offsetHeight - 5;
			if (top < 0) top = coords.top + target.offsetHeight + 5;

			tooltipElem.style.left = left + 'px';
			tooltipElem.style.top = top + 'px';
		};

		document.onmouseout = function (e) {
			if (tooltipElem) {
				tooltipElem.remove();
				tooltipElem = hull;
			}
		};
	});
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

<style>
	.btn {
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
