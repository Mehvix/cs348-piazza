<script>
    import ALL_POSTS from "../cs348-fall-2017.json";

    ALL_POSTS.sort((a, b) => b.result.nr - a.result.nr);

    function getStudents() {
        const students = [].concat(
            ...posts.map((post) =>
                [].concat(
                    post.tag_good || [],
                    post.tag_endorse || [],
                    getStudents(post.children)
                )
            )
        );

        const ids = new Set();

        for (const student of students) {
            const { id } = student;
        }

        return students.filter((id) => {
            if (ids.has(id)) {
                return false;
            }
            ids.add(id);
            return true;
        });
    }

    import Header from "./Header.svelte";
    import Sidebar from "./Sidebar.svelte";
    import Content from "./Content.svelte";

    export function changeQuestion(nr) {
        selected = nr;
        window.location.hash = nr;
    }

    function titles() {
        return posts.map(({ nr, history: [{ subject }] }) => ({
            nr,
            subject,
        }));
    }

    function students() {
        getStudents(posts).reduce(
            (acc, student) => Object.assign(acc, { [student.id]: student }),
            {}
        );
    }

    export let posts = ALL_POSTS.map(({ result }) => result);
    export let selected = 28;
    // export let nr;
</script>

<Header title="CS348" />
<div class="content">
    <Sidebar
        posts={titles()}
        {selected}
        on:select={changeQuestion(window.nr)}
    />
    <Content post={posts.find((nr) => nr === selected)} {students} />
</div>

<style>
    .content {
        display: flex;
        flex-direction: row;
    }
</style>
