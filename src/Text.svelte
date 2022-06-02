<script>
    import katex from "katex";
    import he from "he";

    export let content;
    export let rendered;
    $: rendered = (html) =>
        html.replace(/\$\$[^$]+\$\$/g, (equation) => {
            const ren = katex.renderToString(he.decode(equation.slice(2, -2)));
            console.log(ren);
            return ren;
        });
</script>

<div bind:this={content}>
    {@html rendered}
</div>
