<script>
	import Button from '$lib/Input/Button.svelte';
	import Otp from '$lib/Input/Otp.svelte';
	import { createForm } from 'svelte-forms-lib';
	import * as yup from 'yup';

	let timer = 10 * 60;
    //Show timer in mm:ss format with pad start
    $: time = `${Math.floor(timer / 60)
        .toString()
        .padStart(2, '0')}:${(timer % 60).toString().padStart(2, '0')}`;
	let interval = setInterval(() => {
		timer = timer - 1;
		if (timer == 0) {
			clearInterval(interval);
		}
	}, 1000);

	const { form, handleChange, errors, isSubmitting, handleSubmit } = createForm({
		initialValues: {
			value1: '',
			value2: '',
			value3: '',
			value4: '',
			value5: '',
			value6: ''
		},
		validationSchema: yup.object().shape({
			value1: yup.string().required(),
			value2: yup.string().required(),
			value3: yup.string().required(),
			value4: yup.string().required(),
			value5: yup.string().required(),
			value6: yup.string().required()
		}),
		onSubmit: (values) => {
			console.log(JSON.stringify(values, null, 2));
		}
	});
    $: console.log($form);
</script>

<form on:submit={handleSubmit} class="wrapper">
	<div class="otpLabel">
		Enter OTP
		<div class="time">
			<p>{time}</p>
		</div>
	</div>
	<div class="otp_wrapper">
		<Otp
			name="value1"
			placeholder=""
			type="text"
			error={$errors.value1}
			change={handleChange}
			value={$form.value1}
		/>
		<Otp
			name="value2"
			placeholder=""
			type="text"
			error={$errors.value2}
			change={handleChange}
			value={$form.value2}
		/>
		<Otp
			name="value3"
			placeholder=""
			type="text"
			error={$errors.value3}
			change={handleChange}
			value={$form.value3}
		/>
		<Otp
			name="value4"
			placeholder=""
			type="text"
			error={$errors.value4}
			change={handleChange}
			value={$form.value4}
		/>
		<Otp
			name="value5"
			placeholder=""
			type="text"
			error={$errors.value5}
			change={handleChange}
			value={$form.value5}
		/>
		<Otp
			name="value6"
			placeholder=""
			type="text"
			error={$errors.value6}
			change={handleChange}
			value={$form.value6}
		/>
	</div>

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
	.otp_wrapper {
		display: flex;
		justify-content: space-between;
		width: 100%;
		margin-bottom: 3rem;
		gap: 2rem;
	}
	.otpLabel {
		font-size: 16px;
		font-weight: 500;
		justify-content: space-between;
		display: flex;
	}
	.time p {
		font-size: 16px;
		font-weight: 600;
		color: var(--primary);
	}
</style>
