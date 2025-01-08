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
          <svg class="w-8 h-8" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
            {#if icon === 'rectangle'}
              <rect x="4" y="6" width="16" height="12" rx="2" class="group-hover:fill-gray-100" />
            {:else if icon === 'box'}
              <rect x="4" y="4" width="16" height="16" rx="2" class="group-hover:fill-gray-100" />
            {:else if icon === 'triangle'}
              <path d="M12 4 
                      A 1 1 0 0 1 13 5 
                      L19.5 19
                      A 1 1 0 0 1 18.5 20
                      L5.5 20
                      A 1 1 0 0 1 4.5 19
                      L11 5
                      A 1 1 0 0 1 12 4" 
                    class="group-hover:fill-gray-100" />
            {:else if icon === 'circle'}
              <circle cx="12" cy="12" r="8" class="group-hover:fill-gray-100" />
            {/if}
          </svg>
        </button>
      {/each}
    </div>
  </div>
</nav> 