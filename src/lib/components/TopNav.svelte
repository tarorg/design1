<script lang="ts">
  let isDropdownOpen = false;
  let isProductDropdownOpen = false;
  
  const workspace = { id: 4, name: 'Settings', icon: '⚙️' };
  const teams = [
    { id: 0, name: 'Space', icon: '🌌' }, // Added Space at the top
    { id: 1, name: 'Sale', icon: '⭐' },
    { id: 2, name: 'Products', icon: '📦' },
    { id: 3, name: 'Posts', icon: '🥁' }, // Changed to another drum icon
    { id: 5, name: 'Links', icon: '🔗' },
    { id: 6, name: 'Path', icon: '🌀' }, // Changed to a smooth curve-like icon
    { id: 7, name: 'Analytics', icon: '📈' }, // Changed to a line graph icon
    workspace
  ];

  let currentTeam = teams[0];

  const products = [
    { id: 1, name: 'Design System' },
    { id: 2, name: 'Analytics' },
    { id: 3, name: 'Developer API' }
  ];

  let currentProduct = products[0];

  function toggleDropdown() {
    isDropdownOpen = !isDropdownOpen;
    if (isDropdownOpen) isProductDropdownOpen = false;
  }

  function toggleProductDropdown() {
    isProductDropdownOpen = !isProductDropdownOpen;
    if (isProductDropdownOpen) isDropdownOpen = false;
  }

  function selectTeam(team: typeof teams[0]) {
    currentTeam = team;
    isDropdownOpen = false;
  }

  function selectProduct(product: typeof products[0]) {
    currentProduct = product;
    isProductDropdownOpen = false;
  }
</script>

<header class="fixed top-0 left-0 right-0 bg-white">
  <div class="relative border-b border-gray-200">
    <button 
      class="flex items-center w-full px-4 py-3 hover:bg-gray-50"
      on:click={toggleDropdown}
    >
      <div class="flex items-center flex-1">
        <div class="flex items-center gap-3">
          <div class="w-8 h-8 flex items-center justify-center bg-gray-100 rounded-lg">
            {currentTeam.icon}
          </div>
          <div>
            <div class="font-semibold">{currentTeam.name}</div>
          </div>
        </div>
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

  {#if !isDropdownOpen}
    <div class="relative">
      <button 
        class="flex items-center w-full px-4 py-3 hover:bg-gray-50 border-b border-gray-200"
        on:click={toggleProductDropdown}
      >
        <div class="flex items-center flex-1">
          <div class="flex items-center gap-3">
            <div class="font-semibold">{currentProduct.name}</div>
          </div>
        </div>
      </button>

      {#if isProductDropdownOpen}
        <div 
          class="relative bg-white border-b border-gray-200 shadow-lg"
        >
          <div class="py-2 px-4">
            <div class="text-sm font-medium text-gray-500 mb-3">Products</div>
            <ul class="space-y-2">
              {#each products as product}
                <li>
                  <button
                    class="flex items-center w-full px-3 py-2 rounded-lg hover:bg-gray-50"
                    class:bg-gray-50={currentProduct.id === product.id}
                    on:click={() => selectProduct(product)}
                  >
                    <div class="flex items-center gap-3 flex-1">
                      <span>{product.name}</span>
                    </div>
                    {#if currentProduct.id === product.id}
                      <span class="text-sm text-gray-400">⌘ {product.id}</span>
                    {/if}
                  </button>
                </li>
              {/each}
              <li>
                <button
                  class="flex items-center gap-3 w-full px-3 py-2 rounded-lg hover:bg-gray-50 text-gray-500"
                >
                  <span>Add product</span>
                </button>
              </li>
            </ul>
          </div>
        </div>
      {/if}
    </div>
  {/if}
</header> 