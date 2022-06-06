<script>
    import katex from "katex";
    import he from "he";

    // todo fix scrolling issue caused by katex
    export let rendered;
    $: rendered = () => {
        input = input.replace(/\$\$([^$]+)\$\$/g, (eq) => {
            return katex.renderToString(he.decode(eq.slice(2, -2)));
        });
        input = input.replace(/&#64;(\d+)/g, `<a href=#\$1>@\$1</a>`);
        return input;
    };

    export let input;
</script>

<div>
    {@html rendered()}
</div>
