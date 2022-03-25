<script context="module">
	export function load({ error }) {
		return {
			props: { message: error.message }
		}
	}
</script>

<script>
	export let message
</script>

<div class="error">
	<h2>This page does not exist</h2>
	<p>{message}</p>
	<!-- TODO style button here -->
	<a href="/"><button>Homepage</button></a>
</div>
