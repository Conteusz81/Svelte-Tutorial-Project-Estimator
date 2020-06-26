<script>
    import { createEventDispatcher } from 'svelte';
    import materialStore from '../store/material-store.js';

    const dispatch = createEventDispatcher();
    let materials = [];

    materialStore.subscribe(items => {
        materials = items;
    });

    const currency = new Intl.NumberFormat('pl', { style: 'currency', currency: 'PLN' });

    $: priceSum = materials.reduce((prev, next) => {
        prev += next.price;
        return prev;
    }, 0);
    
    function edit(id, name, price) {
        dispatch('edit', {id, name, price});
    }


</script>
<style>
    table {
        width: 100%;
    }
    tr.product-row {
        cursor: pointer;
    }
</style>

<table class="primary">
    <thead>
    <tr>
        <th>Materiał</th>
        <th>Cena</th>
        <th></th>
    </tr>
    </thead>
    <tbody>
        {#each materials as material (material.id)}
            <tr on:click={edit(material.id, material.name, material.price)}  class="product-row">
                <td>{material.name.toUpperCase()}</td>
                <td>{currency.format(material.price)}</td>
                <td><i class="fa fa-trash-o" aria-hidden="true"></i></td>
            </tr>
        {/each}
    </tbody>
    {#if materials.length > 1}
        <tfoot>
        <tr>
            <td>SUMA</td>
            <td colspan="2">{currency.format(priceSum)}</td>
        </tr>
        </tfoot>
    {/if}
</table>
