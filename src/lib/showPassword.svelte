<script>
	import { onMount } from 'svelte';

	let form;
	let inputsPassword;
	let isShow = false;

	onMount(() => {
		form = document.getElementById('form2');
		inputsPassword = form.querySelectorAll('input[type="password"]');
	});

	function showPassword(e) {
		let line = e.target.closest('.form__line');
		let input = line.querySelector('.form__input');
		if (input.type == 'password') {
			isShow = true;
			input.type = 'text';
		} else {
			isShow = false;
			input.type = 'password';
		}
	}

	function security(e) {
		const input = e.target;
		const container = input.closest('.form__line-container');
		const svgBtn = container.querySelector('.show-password__btn');
		const message = container.querySelector('.form__message');

		if (input.value.length < 5) {
			changeMessage('Password must be at least 4 characters long', '#000');
		} else {
			securityMessage(securityLevel(input.value));
		}

		function securityMessage(level) {
			if (level == 4) {
				changeMessage('Password is Impossible', '#2bff00');
			} else if (level == 3) {
				changeMessage('Password is Strong', '#f2ff00');
			} else if (level == 2) {
				changeMessage('Password is Normally', '#ffa600');
			} else if (level == 1) {
				changeMessage('Password is Easily', 'red');
			} else {
				changeMessage();
			}
		}

		function changeMessage(text = '', color = '#000') {
			message.textContent = text;
			message.style.color = color;
			input.style.borderColor = color;
			svgBtn.style.fill = color;
		}

		function securityLevel(value) {
			const numbers = (value.match(/\d/g) ?? '').length >= 1;
			const signs = (value.match(/[^\b\d\w]/g) ?? '').length >= 1;
			const upperCase = (value.match(/[A-Z]/g) ?? '').length >= 1;
			const lowerCase = (value.match(/[a-z]/g) ?? '').length >= 3;
			return [numbers, signs, upperCase, lowerCase].filter((el) => el == true).length;
		}
	}
</script>

<form action="" class="form" id="form2">
	<p class="form__title">Password</p>

	<div class="form__line-container">
		<div class="form__line">
			<input
				class="form__input"
				type="password"
				id="password"
				placeholder="Введите пароль"
				on:input={security}
			/>
			<label class="form__label" for="password"></label>

			<button type="button" class="show-password__btn" on:click={showPassword}>
				{#if !isShow}
					<svg
						xmlns="http://www.w3.org/2000/svg"
						width="16"
						height="16"
						class="show-password__svg"
						viewBox="0 0 16 16"
					>
						<path
							d="M16 8s-3-5.5-8-5.5S0 8 0 8s3 5.5 8 5.5S16 8 16 8M1.173 8a13 13 0 0 1 1.66-2.043C4.12 4.668 5.88 3.5 8 3.5s3.879 1.168 5.168 2.457A13 13 0 0 1 14.828 8q-.086.13-.195.288c-.335.48-.83 1.12-1.465 1.755C11.879 11.332 10.119 12.5 8 12.5s-3.879-1.168-5.168-2.457A13 13 0 0 1 1.172 8z"
						/>
						<path
							d="M8 5.5a2.5 2.5 0 1 0 0 5 2.5 2.5 0 0 0 0-5M4.5 8a3.5 3.5 0 1 1 7 0 3.5 3.5 0 0 1-7 0"
						/>
					</svg>
				{:else}
					<svg
						xmlns="http://www.w3.org/2000/svg"
						width="16"
						height="16"
						class="show-password__svg"
						viewBox="0 0 16 16"
					>
						<path
							d="M13.359 11.238C15.06 9.72 16 8 16 8s-3-5.5-8-5.5a7 7 0 0 0-2.79.588l.77.771A6 6 0 0 1 8 3.5c2.12 0 3.879 1.168 5.168 2.457A13 13 0 0 1 14.828 8q-.086.13-.195.288c-.335.48-.83 1.12-1.465 1.755q-.247.248-.517.486z"
						/>
						<path
							d="M11.297 9.176a3.5 3.5 0 0 0-4.474-4.474l.823.823a2.5 2.5 0 0 1 2.829 2.829zm-2.943 1.299.822.822a3.5 3.5 0 0 1-4.474-4.474l.823.823a2.5 2.5 0 0 0 2.829 2.829"
						/>
						<path
							d="M3.35 5.47q-.27.24-.518.487A13 13 0 0 0 1.172 8l.195.288c.335.48.83 1.12 1.465 1.755C4.121 11.332 5.881 12.5 8 12.5c.716 0 1.39-.133 2.02-.36l.77.772A7 7 0 0 1 8 13.5C3 13.5 0 8 0 8s.939-1.721 2.641-3.238l.708.709zm10.296 8.884-12-12 .708-.708 12 12z"
						/>
					</svg>
				{/if}
			</button>
		</div>
		<p class="form__message"></p>
	</div>
</form>

<style>
	* {
		margin: 0;
		box-sizing: border-box;
	}
	.form {
		display: flex;
		flex-direction: column;
		gap: 20px;
		width: 300px;
		border: 1px solid #000;
		padding: 20px;
	}
	.form__title {
		font-size: 22px;
		font-weight: 700;
		margin: 0;
	}
	.form__line {
		position: relative;
		width: 100%;
		margin-bottom: 3px;
	}
	.form__label {
		display: flex;
		flex-direction: column;
	}
	.form__input {
		width: 100%;
		padding: 10px 10px;
		border: 2px solid #000;
		border-radius: 5px;
		font-size: 16px;
	}
	.form__input:focus {
		outline: none;
	}
	.show-password__btn {
		position: absolute;
		top: 50%;
		transform: translateY(-50%);
		right: 0;
		border: none;
		background: transparent;
		cursor: pointer;
	}
	.show-password__svg {
		fill: inherit;
		display: block;
		width: 100%;
		height: 100%;
	}
	.form__message {
		font-weight: 700;
		font-size: 14px;
		transition: color 0.3s;
	}
</style>
