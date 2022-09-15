<script>
	import Header1 from '$lib/Headers/Header1.svelte';
import RegistrationForm from '$lib/User/RegistrationForm.svelte';
</script>

<section>
	<Header1 />
	<div class="image_wrapper">
		<img src="https://cdn.dribbble.com/userupload/3074012/file/original-3cba3b2aadcfd5d18bad3c539be599d2.jpeg?compress=1&resize=1024x768" alt="" />
	</div>
	<div class="form_wrapper">
		<div class="page_description">
			<p class="title">Create an <span class="primary_color">Account</span></p>
			<p class="description">
				Welcome to Eyeconit, your one stop destination for eye catcing icons that can be used in
				your code easily. Sign up by providing us your details below
			</p>
		</div>
		<RegistrationForm />
	</div>
</section>

<style>
	section {
		display: flex;
	}

	.form_wrapper {
		width: 60%;
		height: 100vh;
		padding: 120px 150px;
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
		margin: 25px 0;
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
