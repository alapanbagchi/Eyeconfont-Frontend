<script>
	import { page } from '$app/stores';

	let text = 'Log In';
	let link = '/login';
	if ($page.url.pathname.split('/')[1] == 'register') {
		text = 'Log In';
		link = '/login';
	} else {
		text = 'Register';
		link = '/register';
	}
</script>

<header>
	<nav>
		<ul>
			<li>
			</li>
			
		</ul>
	</nav>
</header>

<style>
	header {
		position: absolute;
		width: 100%;
		height: 70px;
		display: flex;
		align-items: center;
		padding: 0 100px;
	}
	nav {
		width: 100%;
		display: flex;
		justify-content: space-between;
	}
	ul {
		width: 100%;
		display: flex;
		justify-content: space-between;
		align-items: center;
		list-style: none;
	}
</style>
