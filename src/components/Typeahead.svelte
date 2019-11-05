<svelte:options tag="arc-typeahead" />
<input placeholder="Search by Name" bind:value={query} type="text" on:keyup={change} />

{#if results}
<small>{count}</small>
    {#if results.length}
        {#each results as result}
            <h3>{result}</h3>
        {/each}
    {:else}
        No results for search term {query}
    {/if}
{/if}

<script>
    import { createEventDispatcher } from 'svelte';
	const dispatch = createEventDispatcher();
    export let results;
    export let event;
    let query;
    let timeoutId;
    function change () {
        if (query.length >= 3) {
            timeoutId && window.clearTimeout(timeoutId);
            timeoutId = window.setTimeout(() => {
                results = null;
                event && window.dispatchEvent(new CustomEvent(event, {detail: query}));
                dispatch('change', query);
            }, 300);
        }
    }
    $: count = results ? results.length : 0;
</script>