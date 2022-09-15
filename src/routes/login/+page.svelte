<script>
	import LoginForm from '$lib/User/LoginForm.svelte';
</script>

<section>
	<div class="image_wrapper">
		<img
			src="https://images.unsplash.com/photo-1620641788421-7a1c342ea42e?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=774&q=80"
			alt=""
		/>
	</div>
	<div class="form_wrapper">
		<div class="page_description">
			<p class="title"><span class="primary_color">Sign In</span></p>
			<p class="description">Welcome back! Enter your credentials to login</p>
		</div>
		<LoginForm />
	</div>
</section>

<style>
	section {
		display: flex;
	}

	.form_wrapper {
		width: 50%;
		height: 100vh;
		padding: 150px 120px;
		max-width: 900px;
		min-width: 900px;
		margin-left: auto;
		margin-right: auto;
	}
	.image_wrapper {
		width: 50%;
		height: 100vh;
		overflow: hidden;
	}
	.image_wrapper img {
		width: 100%;
		height: 100%;
		object-fit: cover;
	}
	.title {
		font-size: 1.6em;
		font-weight: 600;
	}
	.primary_color {
		color: var(--primary);
	}
	.description {
		margin: 20px 0;
		line-height: 30px;
		font-size: 0.9em;
		opacity: 0.7;
		font-weight: 500;
	}
	@media screen and (max-width: 900px) {
		.image_wrapper {
			display: none;
		}
		.form_wrapper {
			width: 100%;
			padding: 100px 20px;
			max-width: none;
			min-width: unset;
		}
	}
</style>
