<script lang="ts">
	import Button from '$lib/Input/Button.svelte';
	import Input from '$lib/Input/Input.svelte';
	import API from '../../utils/API';
	import { createForm } from 'svelte-forms-lib';
	import * as yup from 'yup';
	import { alert } from '../../stores/Notifications';
	const { form, handleChange, errors, touched, isSubmitting, handleSubmit } = createForm({
		initialValues: {
			fullName: '',
			email: '',
			password: '',
			confirmPassword: ''
		},
		validationSchema: yup.object().shape({
			fullName: yup.string().required('Full name is required'),
			email: yup
				.string()
				.required('Email is required')
				.email('Please provide a valid email address'),
			password: yup
				.string()
				.required('Password is required')
				.min(10, 'Password must be at least 10 characters')
				.max(50, 'Password must be at most 50 characters')
				.matches(/(?=.*[A-Z])/, 'Password must contain one uppercase letter')
				.matches(/(?=.*[a-z])/, 'Password must contain one lowercase letter')
				.matches(/(?=.*[0-9])/, 'Password must contain one number')
				.matches(/(?=.*[!@#$%_^&*])/, 'Password must contain one special character'),
			confirmPassword: yup
				.string()
				.required('Confirm password is required')
				.oneOf([yup.ref('password'), null], 'Passwords must match')
		}),

		onSubmit: async (values) => {
			try {
				const canRegister = await API.post('/user/canRegister', values);
				if (canRegister) {
					const response = await API.post('/user/register', values);
					if (response) {
						$alert.title = 'Registration Successful';
						$alert.description = 'You have been successfully registered. Please login to continue.';
						$alert.type = 'SUCCESS';
					}
				}
			} catch (err: any) {
				if (err.response.data.msg == 'USER_EXISTS') {
					$alert.title = 'Registration Failed';
					$alert.description = 'This email is already registered with us. Try logging in instead';
					$alert.type = 'ERROR';
				} else {
					$alert.title = 'Registration Failed';
					$alert.description = 'Something went wrong. Please try again later';
					$alert.type = 'ERROR';
				}
			}
		}
	});
	$: console.log($isSubmitting);
</script>

<form on:submit={handleSubmit} class="wrapper">
	<Input
		name="fullName"
		value={$form.fullName}
		label="Full Name"
		error={$errors.fullName}
		change={handleChange}
		placeholder="Ex: John Doe"
		type="text"
	/>
	<Input
		name="email"
		value={$form.email}
		error={$errors.email}
		label="Email Address"
		change={handleChange}
		placeholder="Ex: johndoe@gmail.com"
		type="email"
	/>
	<Input
		name="password"
		value={$form.password}
		error={$errors.password}
		label="Password"
		change={handleChange}
		placeholder="10+ characters, 1 uppercase character, 1 lowercase character, 1 number and 1 special symbol"
		type="password"
	/>
	<Input
		name="confirmPassword"
		value={$form.confirmPassword}
		error={$errors.confirmPassword}
		change={handleChange}
		label="Confirm Password"
		placeholder="10+ characters, 1 uppercase character, 1 lowercase character, 1 number and 1 special symbol"
		type="password"
	/>
	<Button disabled={$isSubmitting} widthFull text="Submit" color="var(--primary)" onClick={() => {}}
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
