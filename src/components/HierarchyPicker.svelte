<svelte:options tag="arc-hp" />
<h1>HP worx!</h1>
{#each options as option}
{option}
{/each}
<script>
import {onMount} from 'svelte';

export let provider;
let options = [];
$: console.warn(provider);
$: options = provider ? provider() : [];
</script>