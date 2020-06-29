<script>
    import materialStore from '../store/material-store.js'

    export let id;
    export let name;
    export let price;
    export let mode;

    $: canSubmit = name !== "" && price >= 0;

    function submit() {
        if (!canSubmit) { return; }

        console.log(mode);

        if (mode === 'dodaj') {
            materialStore.add(name, +price.toFixed(2))
        }

        if (mode === 'edytuj') {
            materialStore.edit(id, name, price);
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
        <label for="nameField">Materiał</label>
        <input type="text" id="nameField" placeholder="Drewno Klej Etc." bind:value={name}/>

        <label for="priceField">Cena</label>
        <input type="number" id="priceField" placeholder="Cena" min="0" step="any" bind:value={price}/>
    </fieldset>
    <button
       disabled={!canSubmit}
       class="float-right"
       type="submit">
        { mode }
    </button>
    {#if mode === 'edytuj'}
    <button  on:click={cancel} class="float-right" type="button">Anuluj</button>
    {/if}
</form>
