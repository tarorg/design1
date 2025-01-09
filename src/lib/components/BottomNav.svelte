<script lang="ts">
  import { goto } from '$app/navigation';
  import { page } from '$app/stores';

  const navItems = [
    { icon: 'rectangle', path: '/rectangle' },
    { icon: 'box', path: '/box' },
    { icon: 'triangle', path: '/triangle' },
    { icon: 'circle', path: '/circle' }
  ];

  function navigate(path: string) {
    goto(path);
  }
</script>

<nav class="fixed bottom-0 left-0 right-0 bg-white border-t border-gray-200">
  <div class="max-w-screen-xl mx-auto px-4">
    <div class="flex justify-around items-center h-16">
      {#each navItems as {icon, path}}
        <button 
          class="flex items-center justify-center w-full h-full group"
          class:text-blue-600={$page.url.pathname === path}
          on:click={() => navigate(path)}
        >
          <svg class="w-8 h-8" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5">
            {#if icon === 'rectangle'}
              <rect x="4" y="7" width="16" height="10" rx="1" />
            {:else if icon === 'box'}
              <rect x="7" y="7" width="10" height="10" rx="2" />
            {:else if icon === 'triangle'}
              <path d="M12 7L6.5 17h11L12 7z" stroke-linejoin="round" stroke-linecap="round" />
            {:else if icon === 'circle'}
              <circle cx="12" cy="12" r="5" />
            {/if}
          </svg>
        </button>
      {/each}
    </div>
  </div>
</nav> 