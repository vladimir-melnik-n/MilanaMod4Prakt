<h1>My to-do list</h1>
<main>
    <form on:submit|preventDefault={add}>
        <input bind:value={newItem} placeholder="Enter to-do" />
        <button class="add-todo" on:click={add}><span>+</span></button>
    </form>

    <div class="todos">
        {#each todoList as item, index}
        <div class="todo" class:completed={item.completed}>
            <span class="todo__text">{item.task}</span>
            <div class="todo__buttons">
                <button class="complete" on:click={() => complete(index)}>
                    <Icon name="check-mark" />
                </button>
                <button class="delete" on:click={() => remove(index)}>
                    <Icon name="delete" />
                </button>
            </div>
        </div>
        {/each}
    </div>
</main>

<script>
import Icon from '../../../../components/Icon.svelte'

let newItem = "";
let todoList = [];
function add() {
  if (newItem !== "") {
    todoList = [
      ...todoList,
      {
        task: newItem,
        completed: false,
      },
    ];
    newItem = "";
  }
}

function remove(index) {
    todoList.splice(index, 1);
    todoList = todoList;
  }

function complete(index) {
    todoList[index].completed = !todoList[index].completed;
}
</script>

<style>
    main {
    display: flex;
    flex-direction: column;
    align-items: center;
    min-height: 100%;
    padding: 5vmin;
    box-sizing: border-box;
    background: rgb(199, 178, 151);
}

form {
    width: 100%;
    max-width: 500px;
    display: flex;
    align-items: center;
    margin-bottom: 1rem;
	}

input {
    flex-grow: 1;
    width: 0;
    border: none;
    border-bottom: 1px solid rgb(36, 27, 27);
    background: transparent;
    box-shadow: none;
    font-size: 1.2rem;
    margin: 0;
    outline: none;
}

.todos {
		width: 100%;
		max-width: 500px;
	}

.todo {
    display: flex;
    padding: 20px;
    border-radius: 20px;
    box-shadow: 0 0 15px rgba(34, 27, 27, 0.2);
    background-color: hsla(0, 1%, 42%, 0.2);
    margin-top: 1rem;
    font-size: 1.2rem;
    justify-content: space-between;
    align-items: center;
}

.todo__buttons {
    display: flex;
    align-items: center;
    margin-left: 1rem;
}

.todo button {
    width: 32px;
    height: 32px;
    padding: 4px;
    margin: 0;
    flex-shrink: 0;
}

h1 {
    text-align: center;
    font-size: 1.5rem;
    margin: 2em 0;
}


button {
		cursor: pointer;
	}

  	button.add-todo {
		width: 2rem;
		height: 2rem;
		margin: 0;
		background: transparent;
		border: 1px solid black;
		border-radius: 100%;
		flex-shrink: 0;
		margin-left: 1rem;
		cursor: pointer;
	}

	button.add-todo span {
		display: flex;
		align-items: center;
		justify-content: center;
		line-height: 0;
	}
	h1 {
		text-align: center;
		font-size: 1.5rem;
		margin: 2em 0;
	}
	button {
		background-color: transparent;
		border: none;
	}

	button.delete,
	button.delete:hover {
		color: rgb(88, 68, 37);
		transition: color 100ms ease-out;
	}
	button.complete,
	button.complete:hover {
		color: rgb(241, 126, 132);
		transition: color 100ms ease-out;
	}
	.todo.completed {
		color: rgb(54, 125, 196);
	}

	.todo.completed .todo__text {
		text-decoration: line-through;
	}

	.todo.completed button {
		color: rgb(216, 179, 179);
	}
</style>