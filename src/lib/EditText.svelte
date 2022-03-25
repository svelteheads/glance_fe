<script>
	import { onMount } from 'svelte'
	import { createEventDispatcher } from 'svelte'

	const dispatch = createEventDispatcher()

	export let value,
		required = true

	let editing = false,
		original

	onMount(() => {
		original = value
	})

	const edit = () => {
		editing = true
	}

	const keydown = (event) => {
		if (event.key == 'Escape') {
			event.preventDefault()
			value = original // Return name to original value (cancel edit)
			editing = false
		} else if (event.key == 'Enter') {
			finishEdit()
		}
	}

	const finishEdit = () => {
		editing = false
		dispatch('editDone')
	}

	const focus = (element) => {
		element.focus()
	}
</script>

{#if editing}
	<form on:submit|preventDefault on:keydown={keydown} novalidate>
		<textarea bind:value on:blur={finishEdit} {required} use:focus />
	</form>
{:else}
	<div on:click={edit} class="edit-div">
		{value}
	</div>
{/if}

<style>
	textarea {
		resize: none;
		overflow: hidden;
		border: none;
		background: none;
		width: 100%;
		/* TODO fix font size here */
		font-size: inherit;
		font-family: inherit;
		color: inherit;
		font-weight: inherit;
		text-align: inherit;
		box-shadow: none;
		outline: none;
	}
</style>
