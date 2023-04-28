<script>
    import { each } from "svelte/internal";

    let todo = [];
    let item = '';
    function addItem() {
        todo = todo.concat(item);
    }
</script>
<h1>TODO</h1>
<ul>
    {#each todo as object}
    <div style=display:flex;>
        <button>X</button> <li>{object}</li>
    </div>
    {/each}
    <input bind:value={item}>
    <button on:click={addItem}>Add Item</button>
</ul>