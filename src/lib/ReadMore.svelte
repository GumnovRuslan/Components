<script>
	import { onMount } from 'svelte';

	export let id = '0';
	let card;
	let textLength = 300;

	onMount(() => {
		card = document.getElementById(id);
		addEventReadMore(card);
	});

	function addEventReadMore(card) {
		let elCardText;
		let elBtnMore;
		let elDots;
		let elRemainder;
		let fullTextHeight;
		let lowTextHeight;

		elCardText = card.querySelector('.card-info__text');
		fullTextHeight = elCardText.scrollHeight;
		elBtnMore = card.querySelector('.card-info__btn-more');
		createCardMore();
		elBtnMore.addEventListener('click', clickBtn);

		function clickBtn() {
			if (elRemainder.style.visibility == 'hidden') {
				elDots.style.display = 'none';
				elRemainder.style.visibility = 'visible';
				elRemainder.style.opacity = '1';
				elBtnMore.textContent = 'Скрыть';
				elCardText.style.height = `${fullTextHeight}px`;
			} else {
				elDots.style.display = 'inline';
				elRemainder.style.visibility = 'hidden';
				elRemainder.style.opacity = '0';
				elBtnMore.textContent = 'Побробнее';
				elCardText.style.height = `${lowTextHeight}px`;
			}
		}

		function createCardMore() {
			let cardText = elCardText.textContent;
			elCardText.textContent = cardText.slice(0, textLength);
			lowTextHeight = elCardText.scrollHeight;
			elCardText.style.height = `${lowTextHeight}px`;

			let remainder = createElementRemainder(cardText.slice(textLength));
			let dots = createElementDots();

			elCardText.append(dots);
			elCardText.append(remainder);
		}

		function createElementDots() {
			elDots = document.createElement('span');
			elDots.textContent = '...';
			elDots.classList.add('card-info__dots');
			return elDots;
		}
		function createElementRemainder(text) {
			elRemainder = document.createElement('span');
			elRemainder.textContent = text;
			elRemainder.className = 'card-info__remainder';
			elRemainder.style.visibility = 'hidden';
			elRemainder.style.opacity = '0';
			elRemainder.style.transition = '0.4s';
			return elRemainder;
		}
	}
</script>

<div class="card-container">
	<div class="card-info" {id}>
		<p class="card-info__text">
			Lorem ipsum dolor sit amet consectetur adipisicing elit. Aliquam ratione odit, magni
			exercitationem labore illum possimus harum veritatis, error repudiandae vitae, similique velit
			culpa maiores cum libero suscipit commodi animi id ullam optio a illo necessitatibus
			laboriosam? Ratione molestiae non quia ab tenetur, reprehenderit nesciunt. Quaerat voluptates
			dolor corporis nihil cum quod labore culpa quam blanditiis facilis voluptatum eum et iure
			soluta quidem, libero laboriosam fugiat ratione autem recusandae dignissimos mollitia saepe!
			Nemo facilis at tenetur necessitatibus asperiores quas, aut dolorum? Iure accusamus
			necessitatibus ea ipsam odit tempore vitae! Omnis quia minima quae quam est modi veritatis,
			facilis autem repudiandae?
		</p>
		<button class="card-info__btn-more" type="button">Подробнее</button>
	</div>
</div>

<style>
	.card-info {
		padding: 25px;
		width: 350px;
		background: #3943ff;
	}
	.card-info__text {
		font-family: sans-serif;
		margin: 0 0 15px 0;
		color: #f5f5f5;
		overflow: hidden;
		transition: all 0.4s;
	}
	.card-info__btn-more {
		border: 2px solid #f5f5f5;
		background: #3943ff;
		color: #f5f5f5;
		font-size: 16px;
		width: 150px;
		height: 35px;
		cursor: pointer;
		transition: 0.3s;
	}
	.card-info__btn-more:hover {
		transform: scale(1.1);
	}
</style>
