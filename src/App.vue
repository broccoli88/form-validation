<script setup>
	import { ref, onMounted, computed } from "vue";
	import { useVuelidate } from "@vuelidate/core";
	import { required, email, minLength } from "@vuelidate/validators";

	const isFocused = ref({
		username: false,
		password: false,
	});

	const underline = ref();
	const firstInput = ref(null);
	const focus = onMounted(() => {
		firstInput.value.focus();
	});
	const focusOn = (e) => {
		if (e.target.id === "username") {
			isFocused.value.username = true;
			isFocused.value.password = false;
		} else {
			isFocused.value.username = false;
			isFocused.value.password = true;
		}
	};

	// Vuelidate

	const state = ref({
		username: "",
		password: "",
	});

	const rules = {
		username: { minLength: minLength(5), required },
		password: { required },
	};

	const v$ = useVuelidate(rules, state);
	const submitForm = async () => {
		const isFormCorrect = await v$.value.$validate();
		if (!isFormCorrect) return;
		console.log(v$.value);
	};
</script>
<template>
	<div class="container">
		<h1>Sign In</h1>
		<form action="">
			<div class="input-container">
				<label class="label" for="username">Username</label>

				<input
					@click="focusOn"
					ref="firstInput"
					type="text"
					name="username"
					id="username"
					class="input"
					v-model="v$.username.$model"
				/>
				<span
					ref="underline"
					class="input-underline"
					:class="
						isFocused.username
							? 'animate-underlying'
							: 'animate-deunderlying'
					"
				></span>
			</div>
			<span
				class="error"
				v-if="v$.username.$error"
				v-for="error in v$.username.$errors"
			>
				{{ error.$message }}</span
			>
			<div class="input-container">
				<label class="label" for="password">Password</label>

				<input
					v-model="v$.password.$model"
					@click="focusOn"
					type="text"
					name="password"
					id="password"
					class="input"
				/>
				<span
					class="input-underline"
					:class="
						isFocused.password
							? 'animate-underlying'
							: 'animate-deunderlying'
					"
				></span>
			</div>
			<span class="error" v-if="v$.password.$error">
				{{ v$.password.$errors[0].$message }}</span
			>
			<button class="submit" @click.prevent="submitForm">submit</button>
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
		padding: 1rem 2rem;
	}

	.input-container {
		position: relative;
		margin-top: 2rem;
	}

	.input-underline {
		display: block;
		background-color: teal;

		position: absolute;
		bottom: -3px;
		left: 0;
		width: 0%;
		height: 2px;
	}

	.animate-underlying {
		animation: underline 0.6s ease forwards;
	}

	.animate-deunderlying {
		animation: deunderline 0.6s ease;
	}

	@keyframes underline {
		0% {
			width: 0%;
		}

		100% {
			width: 100%;
		}
	}
	@keyframes deunderline {
		0% {
			width: 100%;
		}

		100% {
			width: 0;
		}
	}

	.input {
		/* display: block; */
		width: 100%;
		padding: 0.5rem 1rem;
		background-color: hsl(0, 0%, 14%);
		color: var(--color-text);
		font-size: 1.3rem;
		border: none;
		/* border-radius: 10px; */
		box-shadow: 0 0 10px hsla(0, 0%, 64%, 0.1);
		margin-top: 0.7rem;
		position: relative;
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
		border-color: teal;
		background-color: teal;
		color: white;
	}

	.error {
		margin-top: 0.4rem;
		font-size: 0.8rem;
		display: block;
		color: crimson;
	}
</style>
