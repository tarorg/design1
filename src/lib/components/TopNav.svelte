<script lang="ts">
  import { activeWorkspace } from '$lib/stores/workspace';
  
  let isDropdownOpen = false;
  let isDropdownOpen2 = false;

  const workspace = { id: 4, name: 'Settings', icon: '⚙️' };
  const teams = [
    { id: 0, name: 'Space', icon: '🌌' }, 
    { id: 1, name: 'Sale', icon: '⭐' },
    { id: 2, name: 'Products', icon: '📦' },
    { id: 3, name: 'Posts', icon: '🥁' },
    { id: 5, name: 'Links', icon: '🔗' },
    { id: 6, name: 'Path', icon: '🌀' },
    { id: 7, name: 'Analytics', icon: '📈' },
    workspace
  ];

  let currentTeam = teams[0];
  let currentProduct = 'Product 1'; // Default selected product
  let searchTerm = '';
  const products = ['Product 1', 'Product 2', 'Product 3'];

  function toggleDropdown() {
    isDropdownOpen = !isDropdownOpen;
  }

  function toggleDropdown2() {
    isDropdownOpen2 = !isDropdownOpen2;
  }

  function selectTeam(team: typeof teams[0]) {
    currentTeam = team;
    isDropdownOpen = false;
    $activeWorkspace = team.name.toLowerCase();
  }

  function selectProduct(product: string) {
    currentProduct = product;
    isDropdownOpen2 = false;
  }

  $: filteredProducts = products.filter(product =>
    product.toLowerCase().includes(searchTerm.toLowerCase())
  );
</script>

<header class="fixed top-0 left-0 right-0 bg-white z-10">
  <div class="relative border-b border-gray-200 flex items-center">
    <button 
      class="flex items-center px-4 py-3 hover:bg-gray-50"
      on:click={toggleDropdown}
    >
      <div class="flex items-center gap-3">
        <div class="w-8 h-8 flex items-center justify-center bg-gray-100 rounded-lg">
          {currentTeam.icon}
        </div>
      </div>
    </button>
    <button
      class="flex-grow flex items-center px-4 py-3 hover:bg-gray-50"
      on:click={toggleDropdown2}
    >
      <div class="flex items-center gap-3">
        <span class="font-semibold">{currentProduct}</span>
      </div>
    </button>
  </div>

  {#if isDropdownOpen}
    <div 
      class="fixed inset-0 top-[57px] bottom-[60px] bg-white border-r border-gray-200 shadow-lg flex flex-col"
    >
      <div class="flex-1 overflow-y-auto py-2 px-4">
        <ul class="space-y-2">
          {#each teams.filter(team => team.name !== 'Settings') as team}
            <li>
              <button
                class="flex items-center w-full px-3 py-2 rounded-lg hover:bg-gray-50"
                class:bg-gray-50={currentTeam.id === team.id}
                on:click={() => selectTeam(team)}
              >
                <div class="flex items-center gap-3 flex-1">
                  <div class="w-8 h-8 flex items-center justify-center bg-gray-100 rounded-lg">
                    {team.icon}
                  </div>
                  <span>{team.name}</span>
                </div>
                {#if currentTeam.id === team.id}
                  <span class="text-sm text-gray-400">⌘ {team.id}</span>
                {/if}
              </button>
            </li>
          {/each}
        </ul>
      </div>
      <div class="border-t border-gray-200 bg-white">
        <div class="py-2 px-4">
          <button
            class="flex items-center w-full px-3 py-2 rounded-lg hover:bg-gray-50"
            class:bg-gray-50={currentTeam.name === 'Settings'}
            on:click={() => selectTeam(workspace)}
          >
            <div class="flex items-center gap-3 flex-1">
              <div class="w-8 h-8 flex items-center justify-center bg-gray-100 rounded-lg">
                ⚙️
              </div>
              <span>Settings</span>
            </div>
            {#if currentTeam.name === 'Settings'}
              <span class="text-sm text-gray-400">⌘ 4</span>
            {/if}
          </button>
        </div>
      </div>
    </div>
  {/if}
  {#if isDropdownOpen2}
    <div
      class="fixed inset-0 top-[57px] bottom-[60px] bg-white border-r border-gray-200 shadow-lg flex flex-col"
    >
      <div class="py-2 px-4">
        <input
          type="text"
          class="w-full px-3 py-2 rounded-lg border border-gray-300 focus:outline-none focus:border-indigo-500"
          placeholder="Search Products..."
          bind:value={searchTerm}
        />
      </div>
      <div class="flex-1 overflow-y-auto py-2 px-4">
        <ul class="space-y-2">
          {#each filteredProducts as product}
            <li>
              <button
                class="flex items-center w-full px-3 py-2 rounded-lg hover:bg-gray-50"
                class:bg-gray-50={currentProduct === product}
                on:click={() => selectProduct(product)}
              >
                <div class="flex items-center gap-3 flex-1">
                  <span>{product}</span>
                </div>
                {#if currentProduct === product}
                  <span class="text-sm text-gray-400">⌘ </span>
                {/if}
              </button>
            </li>
          {/each}
        </ul>
      </div>
      <div class="border-t border-gray-200 bg-white">
        <div class="py-2 px-4">
          <button
            class="flex items-center w-full px-3 py-2 rounded-lg hover:bg-gray-50"
            on:click={() => selectProduct('Add Product')}
          >
            <div class="flex items-center gap-3 flex-1">
              <span>Add Product</span>
            </div>
          </button>
        </div>
      </div>
    </div>
  {/if}
</header> 