# Consuming this in vanilla JS

1) npm run build
2) cat public/bundle.js | pbcopy
3) cmd + v into wherever u want to load
4) add the following to the index file

    ```
    <!-- index.html -->
    <arc-typeahead event="movie-result"/>
    <script>
    const movieSearchComponent = document.querySelector('arc-typeahead');
    window.addEventListener('movie-result', function handleMovieSearch(e) {
        return fetch(`https://www.omdbapi.com/?s=${e.detail}&apikey=ed137340`)
        .then((response) => response.json())
        .then(json => json.Search)
        .then(results => results.map(r => r.Title))
        .catch(() => [])
        .then(results => movieSearchComponent.results = results)
    });
    </script>
    ```
