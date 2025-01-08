<script lang="ts">
	import '../app.css';
	import BottomNav from '$lib/components/BottomNav.svelte';
	import TopNav from '$lib/components/TopNav.svelte';
	let { children } = $props();
</script>

<div class="bg-gray-50 min-h-screen">
	<TopNav />
	<div class="pt-14 pb-16">
		{@render children()}
	</div>
</div>

<BottomNav />
