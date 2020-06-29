<script>
    import Form from "./componets/Form.svelte";
    import Table from "./componets/Table.svelte";
    let id;
    let name = "";
    let price = 5;
    $: mode = id ? "edytuj" : "dodaj"

    function edit(ev) {
        ({ id, name, price } = ev.detail)
    }

</script>

<style>
    main {
        flex: 1;
        align-content: center;
        justify-content: center;
        width: 80%;
        margin: 0 auto;
    }
</style>

<main>
    <h1>Project Estimator</h1>
    <Form bind:id bind:name bind:price bind:mode />

    <Table on:edit={edit} bind:mode />
</main>
