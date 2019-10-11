<script>
	export let tag;

function getUrl () {
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

	$: gifPromise = tag && fetch(getUrl())
		.then(res => res.json())
		.then(json => json.data.image_mp4_url);

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
<div class="container" >
	{#await gifPromise}
		<h1>Loading excellent content related to {tag}</h1>
	{:then url}
		<h1>{tag}</h1>
		<video class="gif" width="320" height="240" controls autoplay alt={tag}>
	  		<source src={url} type="video/mp4">
	  	</video>
	{:catch err}
		<small>oops... failed to load that excellent {tag} content</small>
	{/await}
</div>