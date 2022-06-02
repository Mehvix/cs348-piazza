<script>
    import Comment from "./Comment.svelte";
    import Text from "./Text.svelte";

    function question() {
        console.log(post);
        return post.history[0];
    }

    function studentAnswer() {
        console.log(post);
        post.children.find(() => child.type === "s_answer");
    }

    function instructorAnswer() {
        console.log(post);
        return post.children.find(() => child.type === "i_answer");
    }

    function comments() {
        return post.children.filter(() => child.type === "followup");
    }

    function studentName() {
        return post.anon !== "no"
            ? "Anonymous"
            : (students[post.uid] || { name: "Anonymous" }).name;
    }
    export let post;
    export let students;
</script>

<div class="content">
    {#if post}
        <div class="question">
            <h1>{@html question.subject}</h1>
            <main>
                <Text html={question.content} />
            </main>
            <div class="author">
                <span>
                    Good question ({(post.tag_good || []).length})
                </span>
                <span>
                    {studentName(question)}
                </span>
            </div>
        </div>

        {#if studentAnswer}
            <div class="answer">
                <h2>Student Answer</h2>
                <article>
                    <Text html={studentAnswer.history[0].content} />
                </article>
                <div class="author">
                    <span>
                        Thanks! ({(studentAnswer.tag_endorse || []).length})
                    </span>
                    <span>
                        {studentName(studentAnswer.history[0])}
                    </span>
                </div>
            </div>
        {/if}

        {#if instructorAnswer}
            <div class="answer">
                <h2>Instructors Answer</h2>
                <article>
                    <Text html={instructorAnswer.history[0].content} />
                </article>
                <div class="author">
                    {studentName(instructorAnswer)}
                </div>
            </div>
        {/if}

        <div class="comments">
            {#each comments as comment}
                <Comment {comment} {students} />
            {/each}
        </div>
    {:else}
        No post is selected
    {/if}
</div>

<style>
    .content {
        box-sizing: border-box;
        flex-grow: 1;
        padding: 0 32px;
        height: calc(100vh - 40px);
        overflow-y: scroll;
    }

    .author {
        color: #666;
        font-size: smaller;
        text-align: right;
        display: flex;
        flex-direction: row;
        justify-content: space-between;
    }

    .question,
    .answer {
        border: 1px solid #eeeeee;
        padding: 32px;
        margin: 16px 0;
    }

    .comments,
    .question,
    .answer {
        box-sizing: border-box;
        max-width: 710px;
    }
</style>
