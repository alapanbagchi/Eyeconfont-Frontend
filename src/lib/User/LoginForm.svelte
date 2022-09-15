<script lang="ts">
	import Header1 from '$lib/Headers/Header1.svelte';
	import Button from '$lib/Input/Button.svelte';
	import Input from '$lib/Input/Input.svelte';
	import API from '../../utils/API';
	import { createForm } from 'svelte-forms-lib';
	import * as yup from 'yup';
	import { alert } from '../../stores/Notifications';

	let isSubmitting = false;
	const { form, handleChange, errors, touched, handleSubmit } = createForm({
		initialValues: {
			email: 'alapanbagchi.dev@gmail.com',
			password: 'Madv1lla1n_Dash1ng'
		},
		validationSchema: yup.object().shape({
			email: yup
				.string()
				.required('Email is required')
				.email('Please provide a valid email address'),
			password: yup.string().required('Password is required')
		}),

		onSubmit: async (values) => {
			try {
				const login = await API.post('/user/login', values);
				if (login) {
					$alert.title = 'Login Successful';
					$alert.description = 'You have been successfully logged in.';
					$alert.type = 'SUCCESS';
					// window.location.href = './';
				}
			} catch (err: any) {
				switch (err.response.data.msg) {
					case 'USER_DOES_NOT_EXIST': {
						$alert.title = 'User does not exist';
						$alert.description = 'Please check your email address and try again.';
						$alert.type = 'ERROR';
						break;
					}
					case "USER_ALREADY_LOGGED_IN": {
						$alert.title = 'You are already logged in';
						$alert.description = 'Please log out of your current session and try again.';
						$alert.type = 'ERROR';
						break;
					}
					case 'INVALID_PASSWORD': {
						$alert.title = 'Invalid Credentials';
						$alert.description = 'Please check your email and password and try again.';
						$alert.type = 'ERROR';
						break;
					}
					default: {
						$alert.title = 'Login Failed';
						$alert.description = err.response.data.message;
						$alert.type = 'ERROR';
					}
				}
			}
		}
	});
	$: console.log($touched);
</script>

<form on:submit={handleSubmit} class="wrapper">
	<Input
		name="email"
		value={$form.email}
		error={$errors.email}
		label="Email Address"
		change={handleChange}
		placeholder="alapanbagchi.dev@gmail.com"
		type="email"
	/>
	<div class="seperator" />
	<Input
		name="password"
		value={$form.password}
		error={$errors.password}
		label="Password"
		change={handleChange}
		placeholder="10+ characters, 1 uppercase character, 1 lowercase character, 1 number and 1 special symbol"
		type="password"
	/>

	<div class="seperator" />
	<Button disabled={isSubmitting} widthFull color="var(--primary)" onClick={() => {}}
		>Submit</Button
	>
</form>

<style>
	.wrapper {
		display: flex;
		flex-direction: column;
		width: 100%;
	}
</style>
