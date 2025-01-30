<script lang="ts">
    import '../app.css';
    import { onMount, setContext } from 'svelte';
    let { children } = $props();
</script>

{@render children()}