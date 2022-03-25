<script>
	import { supabase } from '../supabase'

	async function signout() {
		const { error } = await supabase.auth.signOut()
	}
</script>

<nav>
	<a href="/"><p>Glance</p></a>
	<button on:click={signout}><span>Logout</span></button>
</nav>

<style>
	nav {
		display: flex;
		justify-content: space-between;
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
