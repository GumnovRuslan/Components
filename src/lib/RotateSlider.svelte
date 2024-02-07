<script>
	let arr = Array.from({ length: 8 }).map((_, i) => ++i);

	function f1(e) {
		let target = e.target;
		let slider = target.closest('.slider');
		slider.style.animationPlayState = 'paused';
	}
	function f2(e) {
		let target = e.target;
		let slider = target.closest('.slider');
		slider.style.animationPlayState = 'running';
	}
</script>

<div class="container">
	<div class="slider">
		{#each arr as num}
			<span style="--i: {num}" class="slider__slide">
				<img
					src="/img/rebecca-3.jpg"
					alt=""
					class="slider__img"
					on:mouseout={f2}
					on:mouseover={f1}
				/>
			</span>
		{/each}
	</div>
</div>

<style>
	.container {
		display: flex;
		align-items: center;
		justify-content: center;
		width: 100vw;
		height: 100vh;
		background: #383838;
		overflow: hidden;
	}

	.slider {
		position: relative;
		width: 200px;
		height: 200px;
		transform-style: preserve-3d;
		animation: rotate 30s linear infinite;
	}

	@keyframes rotate {
		0% {
			transform: perspective(1000px) rotateY(0deg);
		}
		100% {
			transform: perspective(1000px) rotateY(360deg);
		}
	}

	.slider__slide {
		position: absolute;
		top: 0;
		left: 0;
		height: 100%;
		width: 100%;
		cursor: pointer;
		transform-origin: center;
		transform-style: preserve-3d;
		transform: rotateY(calc(var(--i) * 45deg)) translateZ(360px);
	}

	.slider__img {
		position: absolute;
		height: 100%;
		width: 100%;
		object-fit: cover;
		border-radius: 10px;
		top: 0;
		left: 0;
		transition: 2s;
	}

	.slider__img:hover {
		transform: translateY(-50px) scale(1.2);
	}
</style>
