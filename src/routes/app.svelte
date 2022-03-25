<script context="module">
	//export async function load(context) {
	// TODO Fetch todos from API here https://netninja.dev/courses/sveltekit-tutorial/lectures/36982381
	// return {
	// 	status: 301,
	// 	redirect: '/'
	// }
	//}
</script>

<script>
	import { flip } from 'svelte/animate'
	import { dndzone } from 'svelte-dnd-action'
	import EditText from '$lib/EditText.svelte'

	const flipDurationMs = 200

	const handleDndConsider = (e) => {
		todos = e.detail.items
	}
	const handleDndFinalize = (e) => {
		todos = e.detail.items
	}

	let todos = [
		{ id: 11, name: 'item11', done: false },
		{ id: 12, name: 'item12', done: false },
		{ id: 13, name: 'item13', done: false },
		{ id: 14, name: 'item14', done: false },
		{ id: 15, name: 'item15', done: false },
		{ id: 16, name: 'item16', done: false }
		// { id: 17, name: 'item16', done: false },
		// { id: 18, name: 'item16', done: false },
		// { id: 19, name: 'item16', done: false },
		// { id: 20, name: 'item16', done: false },
		// { id: 21, name: 'item16', done: false },
		// { id: 22, name: 'item16', done: false },
		// { id: 23, name: 'item16', done: false },
		// { id: 24, name: 'item16', done: false },
		// { id: 25, name: 'item16', done: false },
		// { id: 26, name: 'item16', done: false },
		// { id: 27, name: 'item16', done: false },
		// { id: 28, name: 'item16', done: false },
		// { id: 29, name: 'item16', done: false },
		// { id: 30, name: 'item16', done: false },
		// { id: 31, name: 'item16', done: false },
		// { id: 32, name: 'item16', done: false },
		// { id: 33, name: 'item16', done: false },
		// { id: 34, name: 'item16', done: false },
		// { id: 35, name: 'item16', done: false }
	]

	const toggleDone = (id) => {
		const todo = todos.find((todo) => todo.id === id)

		if (todo.done == false) {
			todo.done = !todo.done
			todos.push(todos.splice(todos.indexOf(todo), 1)[0]) // Put to end of list
			todos = todos
		} else {
			todo.done = !todo.done
			// TODO move todo out of end of list
			todos = todos
		}
	}

	const deleteDone = () => {
		todos = todos.filter((todo) => todo.done === false)
	}

	// const deleteTodo = (id) => {
	// 	todos = todos.filter((todo) => todo.id !== id)
	// }

	const createMid = (index) => {
		todos.splice(index + 1, 0, { id: 50, name: 'Mid', done: false })
		todos = todos
	}

	const createTop = () => {
		todos = [{ id: 77, name: 'Top', done: false }, ...todos]
	}

	const createBottom = () => {
		todos = [...todos, { id: 90, name: 'Bottom', done: false }]
	}

	// Deletes todos if name is blank
	const deleteBlankTodos = () => {
		todos = todos.filter((todo) => todo.name !== '')
	}
</script>

<svelte:head>
	<title>Glance | Todos</title>
</svelte:head>

<div class="page-content">
	<div class="todos">
		<h1>Your Todos</h1>
		<div class="create-todo create-top" on:click={createTop} />

		<section
			use:dndzone={{ items: todos, flipDurationMs }}
			on:consider={handleDndConsider}
			on:finalize={handleDndFinalize}
		>
			{#each todos as todo (todo.id)}
				<div animate:flip={{ duration: flipDurationMs }}>
					<div
						class="todo-item"
						class:priority={todos.indexOf(todo) <= 2}
						class:done={todo.done == true}
						on:contextmenu|preventDefault={() => toggleDone(todo.id)}
					>
						<EditText bind:value={todo.name} on:editDone={deleteBlankTodos} />
					</div>
					<div class="create-todo create-mid" on:click={() => createMid(todos.indexOf(todo))} />
				</div>
			{/each}
		</section>
		<div class="create-todo create-bottom" on:click={createBottom} />
	</div>

	<!-- {#each todos as todo (todo.id)}
	<p>{todo.name}</p>
{/each} -->

	<button on:click={deleteDone} class="delete-btn">Delete Done</button>
</div>

<style>
	.page-content {
		position: absolute;
		height: 100%;
		width: 100%;
		top: 50%;
		left: 50%;
		transform: translate(-50%, -50%);
	}
	.todos {
		position: absolute;
		top: 50%;
		left: 50%;
		transform: translate(-50%, -50%);
	}
	.todo-item {
		margin: auto;
		display: block;
		background-color: #56e39f;
		border-radius: 64px;
		min-height: 36px;
		padding: 0.5em 1em;
		cursor: pointer;
		font-size: 2rem;
		width: 800px;
	}

	.priority {
		background-color: #ff5e5b;
	}

	.done {
		background-color: rgb(40, 40, 40);
		text-decoration: line-through;
	}

	.delete-btn {
		background-color: transparent;
		cursor: pointer;
		border: 2px solid #ff5e5b;
		border-radius: 64px;
		color: #ff5e5b;
		padding: 16px 48px;
		position: fixed;
		bottom: 0;
	}

	.create-todo {
		cursor: crosshair;
	}

	.create-top {
		height: 40px;
	}

	.create-mid {
		height: 24px;
	}

	.create-bottom {
		height: 80px;
	}
</style>
