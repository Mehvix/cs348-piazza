<script>
    import katex from "katex";
    import he from "he";

    // todo fix scrolling issue caused by katex
    export let rendered;
    // $: rendered = input.replace(/\$\$[^$]+\$\$/g, (equation) => {
    //     const ren = katex.renderToString(he.decode(equation.slice(2, -2)));
    // });
    $: rendered = input;

    export let input;
</script>

<div>
    {@html rendered}
</div>
