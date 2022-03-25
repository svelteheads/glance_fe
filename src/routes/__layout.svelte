<script>
	import '../styles/global.css'
	import Navbar from '$lib/Navbar.svelte'
</script>

<Navbar />
<main>
	<slot />
</main>

<style>
	main {
		margin: auto;
		text-align: center;
		display: block;
	}
</style>
