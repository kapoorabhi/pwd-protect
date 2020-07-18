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
        console.log(formData);
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
        let response = await fetch('http://localhost/8081/data', options);

        let data = await response.json();
        console.log(response);
        // return response.json();
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
        height: 100vh;
        max-width: 1400px;
        background-color: #f9f9f9;
    }

    h1 {
        display: flex;
        justify-content: center;
        border-bottom: 1px solid #e4e4e4;
        padding: 1rem 0.5rem;
        margin: 0;
        text-align: center;
    }

    .form-container {
        display: flex;
        padding: 4em 1em;
        justify-content: center;
        flex-direction: column;   
    }

    .form-group {
        display: flex;
        padding: 1em 0em;
        justify-content: center;
        align-items: center;
    }
</style>

<div class="container">
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
            {JSON.stringify(formData)}

                {#await postResponse}
                    <p>Loading...</p>
                    {:then value}
                        {JSON.stringify(value)}
                    {:catch error}
                    <p>{error.message}</p>
                {/await}
        </div>
    </form>

    <button on:click|preventDefault={handleClick}>Get Data</button>

 

    {#await result}
        <p>Loading...</p>
        {:then value}
            <Table data={value} />
        {:catch error}
        <p>{error.message}</p>
    {/await}
</div>