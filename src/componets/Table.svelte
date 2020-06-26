<script>
    import materialStore from '../store/material-store.js';
    let materials = [];
    materialStore.subscribe(items => {
        materials = items;
    });

    const currency = new Intl.NumberFormat('pl', { style: 'currency', currency: 'PLN' });

    $: priceSum = materials.reduce((prev, next) => {
        prev += next.price;
        return prev;
    }, 0);


</script>
<style>
    table {
        width: 100%;
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
        {#each materials as material}
            <tr id={material.id}>
                <td>{material.name.toUpperCase()}</td>
                <td>{currency.format(material.price)}</td>
                <td><i class="fa fa-trash-o" aria-hidden="true"></i></td>
            </tr>
        {/each}
        {#if materials.length > 1}
            <tr>
                <td>SUMA</td>
                <td colspan="2">{currency.format(priceSum)}</td>
            </tr>
        {/if}
    </tbody>
</table>
