<svelte:options tag='arc-app'/>
<h1>Components</h1>

<!-- <arc-gif tag="dancing" /> -->
<Typeahead results={results} on:change={update} />

<script>
import {onMount} from 'svelte';
import Button from './components/Button.svelte'
import Gif from './components/Gif.svelte'
import Typeahead from './components/Typeahead.svelte'
let results;
function click () {
    alert('clicked');
}
function update (query) {
    results = ['one', 'two', 'three', query.detail];
}

onMount(() => {
    results = [];
});
</script>
