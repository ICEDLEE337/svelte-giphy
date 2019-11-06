<svelte:options tag='arc-app'/>
<h1>Components</h1>

<arc-typeahead results={results} event={event}></arc-typeahead>

<script>
import {onMount} from 'svelte';
import Button from './components/Button.svelte'
import Gif from './components/Gif.svelte'
import Typeahead from './components/Typeahead.svelte'

let results;
const event = 'blah';

function handleMovieSearch(e) {
        return fetch(`https://www.omdbapi.com/?s=${e.detail}&apikey=ed137340`)
        .then((response) => response.json())
        .then(json => json.Search)
        .then(results => results.map(r => r.Title))
        .catch(() => [])
        .then(r => results = r)
}

onMount(() => {
    results = [];
    // const movieSearchComponent = document.querySelector('arc-typeahead');
    window.addEventListener(event, handleMovieSearch);
});
</script>
