<script lang="ts">
  import { activeWorkspace } from '$lib/stores/workspace';
  import Space from '$lib/components/sections/Space.svelte';
  import Sale from '$lib/components/sections/Sale.svelte';
  import Products from '$lib/components/sections/Products.svelte';
  import Posts from '$lib/components/sections/Posts.svelte';
  import Links from '$lib/components/sections/Links.svelte';
  import Path from '$lib/components/sections/Path.svelte';
  import Analytics from '$lib/components/sections/Analytics.svelte';
</script>

<div class="container">
  {#if $activeWorkspace === 'space'}
    <Space />
  {:else if $activeWorkspace === 'sale'}
    <Sale />
  {:else if $activeWorkspace === 'products'}
    <Products />
  {:else if $activeWorkspace === 'posts'}
    <Posts />
  {:else if $activeWorkspace === 'links'}
    <Links />
  {:else if $activeWorkspace === 'path'}
    <Path />
  {:else if $activeWorkspace === 'analytics'}
    <Analytics />
  {/if}
</div>

<style>
  .container {
    padding: 1rem;
    width: 100%;
    height: 100%;
  }
</style> 