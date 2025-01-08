<script lang="ts">
  import { goto } from '$app/navigation';
  import { onMount } from 'svelte';

  onMount(() => {
    goto('/rectangle');
  });
</script>

<main class="min-h-screen pb-16">
  <slot />
</main>
