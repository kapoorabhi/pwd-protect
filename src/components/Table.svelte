<script>
    export let data;
</script>

<style>
    table, th, td {
        border: 1px solid black;
    }

    th, td {
        padding: 0.635rem 1rem;
    }
</style>

<div class="content">
    <div class="table-container">
        <table>
            <tr>
                <th>Id</th>
                <th>Name</th>
                <th>Password</th>
                <th>URL</th>
            </tr>
        {#each data as row}
            <tr>
                <td>{row.id}</td>
                <td>{row.name}</td>
                <td>{row.password}</td>
                <td>{row.url}</td>
            </tr>
        {/each}
        </table>
    </div>
</div>