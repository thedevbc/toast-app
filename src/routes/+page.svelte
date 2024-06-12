<script lang="ts">
    export let data;
    $: message = data.message;
</script>

<h1 class="h1">Welcome to SvelteKit</h1>
<p>Visit <a href="https://kit.svelte.dev">kit.svelte.dev</a> to read the documentation</p>
<p>Here's the message: {message}</p>