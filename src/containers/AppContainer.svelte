<script>
    import Text from '../components/Text';
    import FormField from '../components/FormField';

    let name = '';
    let password = '';
    let url = '';
    let tags = [];

    $: obj = {
        name,
        password,
        url,
        tags: []
    }

    const handleSubmit = () => {
        console.log(obj)
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
            {JSON.stringify(obj)}
        </div>
    </form>
</div>