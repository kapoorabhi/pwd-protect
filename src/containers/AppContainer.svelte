<script>
    import Text from '../components/Text';
    import FormField from '../components/FormField';
    import Table from '../components/Table';

    let name = '';
    let password = '';
    let url = '';
    let tags = '';

    $: formData = {
        name,
        password,
        url,
        tags
    }

    let result = {};
    let postResponse = {};

    const handleSubmit = () => {
        postResponse = submitForm();
        
    }


    const submitForm = async () => {
        const options = {
            method: 'post',
            body: JSON.stringify(formData),
            headers: { 
                'Accept': 'application/json',
                'Content-Type': 'application/json;charset=utf-8',
                "Access-Control-Allow-Origin": "*"
            }
        }
        let response = await fetch('http://localhost:8081/data', options);

        if(response.status === 200 || response.status === 201) {
            return 'Record Saved Successfully!!';
        }
    }

    const handleClick = () => {
        result = getData();
    }

    const getData = async () => {
        let response = await fetch('http://localhost:8081/data');
        let data = response.json();
        return data;
    }

</script>

<style>

    @media only screen and (max-width: 768px) {
        .container {
            padding: 1rem;
        }
    }
    .container {
        margin: 0 auto;
        max-width: 1400px;
        background-color: #f9f9f9;
        display: flex;
        flex-direction: column;
        height: 100%;
        align-items: center;
        overflow: auto;
        padding-bottom: 1rem;
    }
    .content {
        display: flex;
        flex-direction: column;
        min-width: 650px;
        align-items: center;
    }

    h1 {
        display: flex;
        justify-content: center;
        padding: 1rem 0.5rem;
        margin: 0;
        text-align: center;
    }

    .form-container {
        display: flex;
        padding: 3em 2em;
        flex-direction: column;
        align-items: center;
        border: 1px solid #e2e2e2; 
    }

    .form-group {
        display: flex;
        padding: 1em 0em;
        justify-content: center;
        align-items: center;
    }
</style>

<div class="container">
    <div class="content">
        <h1>Welcome to Password protector</h1>
        <form name="pwd" autocomplete="off">
            <div class="form-container">
                <div class="form-group">
                    <Text>Name</Text>
                    <FormField type="text" placeholder="Enter website name" bind:value={name} />
                        </div>
                <div class="form-group">
                    <Text>Password</Text>
                    <FormField type="password" placeholder="Enter your password" bind:value={password} />
                </div>
                <div class="form-group">
                    <Text>URL</Text>
                    <FormField type="text" placeholder="Enter URL" bind:value={url} />
                </div>
                <div class="form-group">
                    <Text>Tags</Text>
                    <FormField type="text" placeholder="Enter related tags" bind:value={tags} />
                </div>
                <button on:click|preventDefault={handleSubmit}>Submit</button>
                {#await postResponse}
                    <p>Saving Records...</p>
                    {:then value}
                        {value}
                    {:catch error}
                    <p>{error.message}</p>
                {/await}
            </div>
        </form>                     
        <button on:click|preventDefault={handleClick}>Get Data</button>
    </div>

    {#await result}
        <p>Loading...</p>
        {:then value}
            <Table data={value} />
        {:catch error}
        <p>{error.message}</p>
    {/await}
</div>