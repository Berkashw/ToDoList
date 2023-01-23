<script>
	let toDoList = []
	let value = ""
	let indexId = 0
	const onKeyPress = (e) => {
		if (e.charCode === 13) addTask()
	}
	function addTask() {
		toDoList = [
			...toDoList,
			{
				id: indexId,
				text: value,
				status: false,
			},
		]
		value = ""
	}
	const removeFirst = () => {
		toDoList = toDoList.slice(1)
	}
	function removeTask(index) {
		toDoList.splice(index, 1)
		toDoList = toDoList
	}
	function removeChecked() {
		toDoList = toDoList.filter((el) => {
			return !el.status
		})
	}
</script>

<main>
	<h2>To Do List for today</h2>
	<input on:keypress={onKeyPress} type="text" bind:value id="taskInput" />
	<button id="addBtn" on:click={addTask}>Add Task</button>
	<button id="removeFirst" on:click={removeFirst}>Remove First task</button>
	<button id="removeChecked" on:click={removeChecked}>Remove Checked </button>
	<br />
	{#each toDoList as item, index}
		{index + 1}<input bind:checked={item.status} type="checkbox" />
		<span class:checked={item.status}>{item.text}</span>
		<span on:click={() => removeTask(index)}>Remove</span>
		<br />
	{:else}
		<p>No tasks for today</p>
	{/each}
</main>

<style>
	.checked {
		text-decoration: line-through;
	}
	p {
		padding-left: 1em;
	}
	main {
		text-align: left;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
	}

	h1 {
		color: #ff3e00;
		text-transform: uppercase;
		font-size: 4em;
		font-weight: 100;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>
