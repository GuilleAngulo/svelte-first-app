<script>
    let value = "";
    let response = [];
    console.log(response);

    const handleInput = (event) => {
        value = event.target.value;
    };

    $: if (value.length > 2) {
        fetch(
            `http://www.omdbapi.com/?apikey=${__myapp.env.API_CLIENT_KEY}&s=${value}`
        )
            .then((res) => res.json())
            .then((apiResponse) => (response = apiResponse.Search));
    }
</script>

<style>
    ul,
    li {
        list-style: none;
    }
    div {
        width: 200px;
        display: flex;
        margin: 0 auto;
        text-align: left;
    }
</style>

<input {value} on:input={handleInput} />
<div>
    <ul>
        {#each response as film}
            <li>{film.Title}</li>
        {/each}
    </ul>
</div>
