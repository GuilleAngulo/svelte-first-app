<script>
    export let index, title, year, poster;
</script>

<style>
    article {
        position: relative;
        padding: 16px;
        margin: 4px;
        border-radius: 10px;
        cursor: pointer;
        border: 0.4px solid #cbd5e0;
        box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1),
            0 2px 4px -1px rgba(0, 0, 0, 0.06);
    }
    article:hover {
        transition: box-shadow 0.2s ease-in-out;
        box-shadow: 0 25px 50px -12px rgba(0, 0, 0, 0.25);
    }
    header {
        display: flex;
        justify-content: center;
        margin-bottom: 12px;
    }
    span {
        color: #a0aec0;
        margin-right: 2px;
    }
    h3 {
        margin: 6px;
        margin-bottom: 0;
        text-align: left;
        align-self: baseline;
    }
    span.index {
        position: absolute;
        margin-top: 4px;
        margin-right: 8px;
        right: 0;
        top: 0;
    }
    span.year {
        align-self: baseline;
    }
</style>

<article>
    <span class="index">{index + 1}</span>
    <header>
        <h3>
            {title}
            {#if new Date().getFullYear() - year < 2}🆕{/if}
        </h3>
        <span class="year">{year}</span>
    </header>
    <img src={poster} alt={title} />
</article>
