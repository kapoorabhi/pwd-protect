<script>
    // export let type;
    // export let modifier;
    export let semantic = 'span';
</script>

<style>
    label, p, span {
        font-size: 1rem;
        min-width: 100px;
        margin: 0 0.625rem;
    }
</style>

{#if semantic === 'label'}
    <label><slot></slot></label>
{:else if semantic === 'p'} 
     <p><slot></slot></p>
{:else} 
    <span><slot></slot></span>
{/if}