<script>
	import { supabase } from '../supabase'

	async function signInWithGoogle() {
		const { user, session, error } = await supabase.auth.signIn({
			provider: 'google'
		})
	}
</script>

<svelte:head>
	<title>Glance</title>
</svelte:head>

<div class="content">
	<h2>We couldn’t find a todo app that worked the way we wanted.</h2>
	<h2>So we built our own.</h2>
	<br />
	<h1>Welcome to Glance</h1>
	<button on:click={signInWithGoogle}>Login with Google</button>
	<!-- TODO Delete app link before release -->
	<h3><a href="/app">App</a></h3>
</div>

<style>
	.content {
		position: absolute;
		top: 50%;
		left: 50%;
		transform: translate(-50%, -50%);
	}
	button {
		background-color: transparent;
		cursor: pointer;
		border: 2px solid #56e39f;
		border-radius: 64px;
		color: #56e39f;
		padding: 16px 48px;
	}
</style>
