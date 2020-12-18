<script>
    import Movie from "./Movie.svelte";

    let value = "";
    let response = [];

    const handleInput = (event) => {
        value = event.target.value;
    };

    $: if (value.length > 2) {
        response = fetch(
            `http://www.omdbapi.com/?apikey=${__myapp.env.API_CLIENT_KEY}&s=${value}`
        )
            //  .then((res) => !res.ok() && new Error("Oops...something is wrong"))
            .then((res) => res.json())
            .then((apiResponse) => apiResponse.Search || []);
    }
</script>

<style>
    section {
        display: grid;
        grid-template-columns: repeat(3, 1fr);
        grid-gap: 16px;
        margin-top: 6px;
    }
    span {
        text-align: left;
    }
    div {
        width: 200px;
        display: flex;
        flex-direction: column;
        margin: 0 auto;
        text-align: left;
    }
</style>

<div>
    <input placeholder="Search movies ..." {value} on:input={handleInput} />
</div>

{#await response}
    <span>Loading...</span>
{:then movies}
    <section>
        {#each movies as { Title, Poster, Year }, index}
            <Movie {index} title={Title} poster={Poster} year={Year} />
        {:else}<span>No results ...</span>{/each}
    </section>
{:catch error}
    <span>❌ {error}</span>
{/await}
