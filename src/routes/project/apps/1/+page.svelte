<script>
    import Icon from "../../../../components/Icon.svelte";
    let newItem = "";
    let todoList = [];
    function add() {
        if (newItem != "") {
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

<main>
    <h1>My to-do list</h1>
    <enhanced:img src="img.jpg" alt="" />
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
                        <!-- <Icon name="complete" /> -->
                        <svg viewBox="0 0 24 24">
                            <path
                                d="M19.77 4.93l1.4 1.4L8.43 19.07l-5.6-5.6 1.4-1.4 4.2 4.2L19.77 4.93m0-2.83L8.43 13.44l-4.2-4.2L0 13.47l8.43 8.43L24 6.33 19.77 2.1z"
                                fill="currentColor"
                            />
                        </svg>
                    </button>
                    <button class="delete" on:click={() => remove(index)}>
                        <svg viewBox="0 0 24 24">
                            <path
                                d="M6 19c0 1.1.9 2 2 2h8c1.1 0 2-.9 2-2V7H6v12zM8 9h8v10H8V9zm7.5-5l-1-1h-5l-1 1H5v2h14V4h-3.5z"
                                fill="currentColor"
                            />
                        </svg>
                    </button>
                </div>
            </div>
        {/each}
    </div>
</main>

<style>
    .add-todo {
        border: 1px solid black;
        border-radius: 100%;
        width: 25px;
        height: 25px;
    }

    button {
        background-color: transparent;
        border: none;
    }
    button.delete,
    button.delete:hover {
        color: brown;
        transition: color 100ms ease-out;
    }
    button.complete,
    button.complete:hover {
        color: cadetblue;
        transition: color 100ms ease-out;
    }

    .todo.completed {
        color: slategray;
    }
    .todo.completed .todo\_\_text {
        text-decoration: line-through;
    }
    .todo.completed button {
        color: silver;
    }

    .todo {
        display: flex;
        padding: 20px;
        border-radius: 20px;
        box-shadow: 0 0 15px rgb(0 0 0 / 20%);
        background-color: hsla(0, 0%, 100%, 0.2);
        margin-top: 1rem;
        font-size: 1.2rem;
        justify-content: space-between;
        align-items: center;
    }
    .todo\_\_buttons {
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
    main {
        display: flex;
        flex-direction: column;
        align-items: center;
        min-height: 100%;
        padding: 5vmin;
        box-sizing: border-box;
        background: antiquewhite;
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
        border-bottom: 1px solid black;
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
</style>
