<svelte:options tag="arc-btn" />
<button on:click>{label}</button>
<script>
export let label;
</script>
<style>
button {
    padding: 16px;
    box-shadow: 5px 5px rgba(0, 0, 0, 0.5);
    background-color: lightgray;
}
</style>