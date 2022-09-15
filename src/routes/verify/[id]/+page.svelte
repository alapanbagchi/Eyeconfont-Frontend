<script lang="ts">
	import Button from '$lib/Input/Button.svelte';
	import API from '../../../utils/API';
	import { page } from '$app/stores';
	import { onMount } from 'svelte';
	let displayPage = false;
	$: error = {
		title: '',
		description: '',
		link: '',
        btn_text: ''
	};
	onMount(async () => {
		try {
			await API.post('user/verify', { otp: $page.params.id });
			displayPage = true;
		} catch (err: any) {
			switch (err.response.data.msg) {
				case 'USER_ALREADY_VERIFIED':
                    window.location.href = '../../'
					break;
				case 'USER_NOT_LOGGED_IN':
					error = {
						title: 'You are not logged in',
						description: 'Please login to verify your account',
						link: '../../login',
                        btn_text: 'Login'
					};
					break;
                case 'UNAUTHORIZED':
                    error = {
                        title: 'You are not logged in',
                        description: 'Please login to verify your account',
                        link: '../../login',
                        btn_text: 'Login'
                    };
                    break;
				case 'INVALID_OTP':
					error = {
						title: 'Invalid OTP',
						description: 'Please enter a valid OTP',
						link: '../../verify',
                        btn_text: 'Resend OTP'
					};
					break;
				case 'USER_NOT_REGISTERED':
					error = {
						title: 'You are not registered',
						description: 'Please register to verify your account',
						link: '../../register',
                        btn_text: 'Register'
					};
					break;
			}
			displayPage = true;
		}
	});
	$: console.log(error.title != '');
</script>

{#if error.title == '' && displayPage}
	<section>
		<div class="image">
			<img width="400px" src="/icons/mailbox.svg" alt="" />
		</div>
		<div class="text">
			<div class="title">
				<p>Your Account Has Been <span class="primary"> Verified </span></p>
			</div>
			<div class="description">
				Your account has been verified. You can now access our website without any restrictions.
				Enjoy!
			</div>
			<a class="cta" target="blank" href="../../">
				<Button color="var(--primary)" widthFull={false} onClick={() => {}}>Go Back</Button>
			</a>
		</div>
	</section>
{:else}
	<section>
		<div class="image">
			<img width="400px" src="/icons/errorpage.svg" alt="" />
		</div>
		<div class="text">
			<div class="title">
				<p>{error.title}</p>
			</div>
			<div class="description">
				{error.description}
			</div>
			<a class="cta" target="blank" href="{error.link}">
				<Button color="var(--primary)" widthFull={false} onClick={() => {}}>{error.btn_text}</Button>
			</a>
		</div>
	</section>
{/if}

<style>
	section {
		width: 100%;
		height: 100vh;
		display: flex;
		flex-direction: column;
		align-items: center;
		padding: 80px 0;
	}
	.text {
		display: flex;
		flex-direction: column;
		align-items: center;
	}
	.title {
		font-size: 1.6em;
		font-weight: 600;
	}
	.primary {
		color: var(--primary);
	}
	.description {
		opacity: 0.8;
		margin: 20px 0;
		width: 600px;
		text-align: center;
		line-height: 30px;
	}
</style>
