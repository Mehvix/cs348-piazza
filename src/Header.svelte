<script>
    export let title;
</script>

<header>{title}</header>
<div class="spacer" />

<style>
    header {
        width: 100%;
        background-color: #3e7aab;
        color: white;
        height: 40px;
        font-size: larger;
        font-weight: bold;
        display: flex;
        align-items: center;
        padding: 0 16px;
        position: fixed;
    }
    .spacer {
        height: 40px;
    }
</style>
