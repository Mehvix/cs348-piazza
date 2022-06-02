<script>
    const Text = "./Text.svelte";

    export let comment;
    export let studentName;
    $studentName: (post) =>
        post.anon !== "no"
            ? "Anonymous"
            : (students[post.uid] || { name: "Anonymous" }).name;
</script>

<div class="comment">
    <div class="author">
        {studentName(comment)}
    </div>
    <Text html={comment.subject} />

    {#each comment.children as response}
        <div class="response">
            <div class="author">
                {studentName(response)}
            </div>
            <Text html={response.subject} />
        </div>
    {/each}
</div>

<style>
    .author {
        color: #666;
        font-size: smaller;
    }

    .comment,
    .response {
        box-sizing: border-box;
        padding: 16px;
        margin: 16px 0;
        border: 1px solid #eeeeee;
        width: 100%;
    }
</style>
