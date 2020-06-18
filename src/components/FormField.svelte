<script>
    export let type = "text";
    export let placeholder = "";
    export let value = ""

    const handleInput = e => {
        value = e.target.value;
        // console.log(value);
    }
</script>

<style>
    input[type='text'],  input[type='password']{
        margin: 0;
        min-width: 300px;
        height: 45px;
        max-height: 50px;
    }
</style>

<input {type} {placeholder} {value} on:input={handleInput} />