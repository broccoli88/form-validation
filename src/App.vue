<script setup>
	import { ref, onMounted } from "vue";

	const firstInput = ref(null);
	const focus = onMounted(() => {
		firstInput.value.focus();
	});
</script>
<template>
	<div class="container">
		<h1>Form</h1>
		<form action="">
			<div class="input-container">
				<label class="label" for="username">Username</label>
				<input
					ref="firstInput"
					type="text"
					name="username"
					id="username"
					class="input"
				/>
			</div>
			<div class="input-container">
				<label class="label" for="password">Password</label>
				<input
					type="text"
					name="password"
					id="password"
					class="input"
				/>
			</div>
			<button class="submit">submit</button>
		</form>
	</div>
</template>
<style scoped>
	.container {
		width: 500px;
		background-color: hsl(0, 0%, 12%);
		box-shadow: 0 0 15px hsla(0, 0%, 74%, 0.1);
		border-radius: 20px;
	}

	.container > h1 {
		font-size: 4rem;
		font-weight: 700;
		text-align: center;
		color: white;
	}

	form {
		display: flex;
		flex-direction: column;
	}

	.input-container {
		padding: 1rem 2rem;
	}

	.input {
		/* display: block; */
		width: 100%;
		padding: 0.5rem 1rem;
		background-color: hsl(0, 0%, 14%);
		color: var(--color-text);
		font-size: 1.3rem;
		border: none;
		border-radius: 10px;
		box-shadow: 0 0 10px hsla(0, 0%, 64%, 0.1);
		margin-top: 0.7rem;
	}

	.input:focus {
		border: 1px solid white;
		outline: none;
	}

	.submit {
		margin: 3rem auto;
		padding: 0.7rem 1.5rem;
		border: 1px solid hsl(0, 0%, 100%, 0.4);
		border-radius: 10px;
		background: none;
		font-size: 1.4rem;
		font-weight: 600;
		letter-spacing: 1px;
		text-transform: capitalize;
		color: var(--color-text);
		cursor: pointer;
		transition: 0.3s all ease;
		outline: none;
	}

	.submit:hover,
	.submit:focus {
		border-color: white;
		background-color: white;
		color: black;
	}
</style>
