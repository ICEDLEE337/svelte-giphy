<script>
	import throttle from 'just-throttle';
	import {fade} from 'svelte/transition';
	export let tag;

function getUrl () {
	// api credit (including key) => https://codepen.io/ChynoDeluxe/pen/WGQzWW
	const giphy = {
		baseURL: "https://api.giphy.com/v1/gifs/",
		apiKey: "0UTRbFtkMxAplrohufYco5IY74U8hOes",
		tag,
		type: "random",
		rating: "pg-13"
	};

	let giphyURL = encodeURI(
		giphy.baseURL +
			giphy.type +
			"?api_key=" +
			giphy.apiKey +
			"&tag=" +
			giphy.tag +
			"&rating=" +
			giphy.rating
	);
	return giphyURL;
}

	let gifPromise;

	let api = () => {
		return fetch(getUrl())
			.then(res => res.json())
			.then(json => json.data.image_mp4_url);
	}

	let loadData = () => {gifPromise = api();};

	loadData();

	let keypress = throttle(loadData, 500);

</script>

<style>
	.gif {
		display: block;
		width: 100%;
		height: 600px;
		margin: auto;
		z-index: 1000000;
	}

	.container {
		display: flex;
		align-content: center;
		justify-content: center;
		flex-direction: column;
	}
</style>

<svelte:options tag="arc-gif" />

<div class="container" in:fade="{{duration: 3000}}" >
	<input type="text" bind:value={tag} on:keypress={keypress}/>
	{#if gifPromise }
		{#await gifPromise}
			<h1>Loading excellent content related to {tag}</h1>
		{:then url}
			<video class="gif" width="320" height="240" controls autoplay alt={tag}>
		  		<source src={url} type="video/mp4">
		  	</video>
		{:catch err}
			<small>oops... failed to load that excellent {tag} content</small>
		{/await}
	{/if}
</div>