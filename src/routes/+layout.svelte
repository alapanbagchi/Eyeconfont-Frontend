<script lang="ts">
	import Notification from '$lib/Notifications/Notification.svelte';
	import API from '../utils/API';
	import { onMount } from 'svelte';
	import '../app.css';
	$: verified = false;
	$: unauth = false
	onMount(async () => {
		try {
			let res = await API.get('user/me', {});
			console.log(res)
			if(res.data.verified) {
				verified = true;
			}
		} catch (err: any) {
			if(err.response.data.msg === 'UNAUTHORIZED') {
				unauth = true;
			}
		}
	});
</script>

<slot />

{verified? 'VERIFIED': 'NOT VERIFIED'}
{unauth? 'UNAUTHORIZED': 'AUTHORIZED'}
<Notification />
