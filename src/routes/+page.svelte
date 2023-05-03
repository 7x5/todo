<script>
    import { each, onMount, text } from "svelte/internal";

    let todo = [
    { done: false, name: 'Fix the todo app' },
    { done: false, name: 'CSS' },
    { done: false, name: 'Present' }
    ];
    onMount(() => {
        const existingTodo = localStorage.getItem('todo');
        todo = JSON.parse(existingTodo) || [];
    });

    function addItem() {
        todo = todo.concat({ done: false, name: '' });
        localStorage.setItem('todo', JSON.stringify(todo));
    }

    function removeItem() {
        todo = todo.filter(i => !i.done)
        localStorage.setItem('todo', JSON.stringify(todo));
    }

    function save() {
        localStorage.setItem('todo', JSON.stringify(todo));
    }

</script>
<h1>TODO</h1>
<ul>
    {#each todo as object}
    <div style=display:flex;>
            <button class="btn" on:click="{object.done = !object.done }" on:click="{removeItem}">X</button> 
            <input class="inp" placeholder="Add TODO here" value={object.name}>
            <select>
                <option value="- SELECT PRIORITY -">- SELECT PRIORITY -</option>
                <option value="Low">Low</option>
                <option value="Medium">Medium</option>
                <option value="High">High</option>
            </select>
    </div>
    {/each}
    <br>
    <button class="submit" on:click={addItem}>Add Item</button>
</ul>

<style>
    * {
        font-family:'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif
    }

    .btn {
        margin-bottom: 5px;
        margin-right: 5px;
        background-color: red;
        border: 1px solid black;
        border-radius: 5px;
        box-shadow: 3px 3px 0px -1px rgba(0, 0, 0, 0.81);
    }

    .btn:active {
        margin-top: 2px;
        box-shadow: 0px 0px 0px -1px rgba(0, 0, 0, 0.81);
    }

    .inp {
        border-radius: 5px;
        margin-bottom: 5px;
        margin-right: 2px;
        border: solid 1px black;
        box-shadow: 2px 2px 0px -1px rgba(0, 0, 0, 0.81);
    }

    .submit {
        background-color: #00cc00;
        border: 1px solid black;
        border-radius: 5px;
        box-shadow:  3px 3px 0px -1px rgba(0, 0, 0, 0.81);
    }

    .submit:active {
        margin-top: 3px;
        box-shadow: 0px 0px 0px -1px rgba(0, 0, 0, 0.81);
    }
</style>