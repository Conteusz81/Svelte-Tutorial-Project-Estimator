<script>
    import materialStore from '../store/material-store.js'

    export let id;
    export let name = "";
    export let price = 5;

    $: mode = id ? "edit" : "add"
    $: canSubmit = name !== "" && price >= 0;

    function submit() {
        if (!canSubmit) { return; }

        if (mode === 'add') {
            materialStore.add(name, price)
        }

       cancel();
    }

    function cancel() {
        price = 5;
        name = "";
        id = undefined;
    }
</script>

<style>
    button {
        margin-left: 20px;
    }

    button:disabled {
        cursor: not-allowed;
    }
</style>

<form on:submit|preventDefault={submit}>
    <fieldset>
        <label for="nameField">Material</label>
        <input type="text" id="nameField" placeholder="Wood, Glue Etc." bind:value={name}/>

        <label for="priceField">Price</label>
        <input type="number" id="priceField" placeholder="Price" min="0" step="any" bind:value={price}/>
    </fieldset>
    <button
       disabled={!canSubmit}
       class="float-right"
       type="submit">
        { mode }
    </button>
    {#if mode === 'edit'}
    <button  on:click={cancel} class="float-right" type="button">Cancel</button>
    {/if}
</form>
