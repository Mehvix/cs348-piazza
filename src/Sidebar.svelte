<script>
    function filteredPosts() {
        return filter
            ? posts.filter(
                  (post) =>
                      post.subject
                          .toLowerCase()
                          .includes(filter.toLowerCase()) || post.nr === +filter
              )
            : posts;
    }

    export let selected;
    export let posts;
    export let filter = "";
</script>

<div class="container">
    <input
        class="search"
        placeholder="Search"
        type="text"
        bind:value={filter}
    />

    {#each filteredPosts() as post}
        <div
            class="post"
            class:selected={post.nr === selected}
            on:click={() => (selected = post.nr)}
            on:click={() => (window.location.hash = post.nr)}
        >
            {@html post.subject}
        </div>
    {/each}
</div>

<style>
    .container {
        width: 300px;
        height: calc(100vh - 40px);
        overflow-y: scroll;
        border-right: 1px solid #eeeeee;
    }

    .search {
        box-sizing: border-box;
        border: none;
        border-bottom: 1px solid #eeeeee;
        height: 30px;
        width: 100%;
        padding: 0 16px;
        margin: 0;
    }

    .post {
        display: flex;
        flex-direction: column;
        justify-content: center;
        border-bottom: 1px solid #eeeeee;
        height: 40px;
        padding: 0 16px;
        cursor: pointer;
        font-size: smaller;
        font-weight: 600;
    }

    .post:hover {
        background-color: #fafafa;
    }

    .selected,
    .selected:hover {
        background: #f0f0f0;
    }
</style>
