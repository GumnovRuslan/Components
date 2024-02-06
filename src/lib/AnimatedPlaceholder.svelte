<script>
	let inputs = [
		{
			type: 'text',
			name: 'Имя',
			required: true,
			id: 'first-name'
		},
		{
			type: 'text',
			name: 'Фамилия',
			required: true,
			id: 'last-name'
		},
		{
			type: 'text',
			name: 'Отчество',
			required: false,
			id: 'surname'
		}
	];
</script>

<form class="form">
	<p class="form__title">Новый клиент</p>

	{#each inputs as input}
		<div class="form__line">
			<input
				type={input.type}
				class="form__input"
				placeholder={input.name}
				id={input.id}
				required={input.required}
			/>
			<label class="form__label" for={input.id}
				>{input.name}
				<span class="form__input-star">*</span>
			</label>
		</div>
	{/each}

	<button class="form__btn-add">Добавить</button>
</form>

<style>
	* {
		box-sizing: border-box;
	}
	.form {
		display: flex;
		flex-direction: column;
		gap: 30px;
		width: 400px;
		padding: 20px;
		border: 1px solid #000;
	}
	.form__title {
		margin: 0;
		text-align: center;
		font-size: 20px;
		font-weight: 700;
	}
	.form__line {
		position: relative;
	}
	.form__label {
		position: absolute;
		top: 0;
		left: 0;
		display: flex;
		align-items: center;
		height: 100%;
		font-size: 16px;
		pointer-events: none;
		border: none;
		transform-origin: 0 0;
		transition: transform 0.25s ease-in-out;
		color: grey;
	}
	.form__input {
		font-family: sans-serif;
		width: 100%;
		min-height: 25px;
		border: none;
		border-bottom: 1px solid grey;
		font-size: 16px;
	}
	.form__input-star {
		display: none;
	}
	.form__input:required ~ .form__label > .form__input-star {
		display: block;
		color: #45c543;
	}
	.form__input:focus ~ .form__label,
	.form__input:not(:placeholder-shown) ~ .form__label {
		top: 0;
		transform: scale(0.85) translate(calc(-0.15rem), -20px);
	}
	.form__input::placeholder {
		font-size: 0;
	}
	.form__btn-add {
		height: 40px;
		width: 160px;
		margin: 0 auto;
		font-weight: 700;
		color: #f5f5f5;
		border: none;
		border-radius: 5px;
		background: #039f00;
		cursor: pointer;
		transition: background 0.2s;
	}
	.form__btn-add:hover {
		background: #45c543;
	}
</style>
