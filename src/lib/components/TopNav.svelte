<script lang="ts">
  let isDropdownOpen = false;
  let isProductDropdownOpen = false;
  
  const teams = [
    { id: 1, name: 'Acme Inc', icon: '📦' },
    { id: 2, name: 'Acme Corp.', icon: '〰️' },
    { id: 3, name: 'Evil Corp.', icon: '✂️' }
  ];

  let currentTeam = teams[0];

  const products = [
    { id: 1, name: 'Design System', icon: '🎨' },
    { id: 2, name: 'Analytics', icon: '📊' },
    { id: 3, name: 'Developer API', icon: '⚡' }
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

<header class="fixed top-0 left-0 right-0 bg-white border-b border-gray-200">
  <div class="relative">
    <button 
      class="flex items-center w-full px-4 py-3 hover:bg-gray-50 border-b border-gray-100"
      on:click={toggleDropdown}
    >
      <div class="flex items-center flex-1">
        <div class="flex items-center gap-3">
          <div class="w-8 h-8 flex items-center justify-center bg-gray-100 rounded-lg">
            {currentTeam.icon}
          </div>
          <div>
            <div class="font-semibold">{currentTeam.name}</div>
            <div class="text-sm text-gray-500">Enterprise</div>
          </div>
        </div>
      </div>
      <svg 
        class="w-5 h-5 text-gray-400 transform transition-transform duration-200" 
        class:rotate-180={isDropdownOpen}
        viewBox="0 0 20 20" 
        fill="currentColor"
      >
        <path fill-rule="evenodd" d="M5.293 7.293a1 1 0 011.414 0L10 10.586l3.293-3.293a1 1 0 111.414 1.414l-4 4a1 1 0 01-1.414 0l-4-4a1 1 0 010-1.414z" clip-rule="evenodd" />
      </svg>
    </button>

    {#if isDropdownOpen}
      <div 
        class="absolute top-full left-0 right-0 bg-white border-b border-gray-200 shadow-lg z-50"
      >
        <div class="p-4">
          <div class="text-sm font-medium text-gray-500 mb-3">Teams</div>
          <ul class="space-y-2">
            {#each teams as team}
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
            <li>
              <button
                class="flex items-center gap-3 w-full px-3 py-2 rounded-lg hover:bg-gray-50 text-gray-500"
              >
                <div class="w-8 h-8 flex items-center justify-center bg-gray-100 rounded-lg">
                  +
                </div>
                <span>Add team</span>
              </button>
            </li>
          </ul>
        </div>
      </div>
    {/if}

    <button 
      class="flex items-center w-full px-4 py-3 hover:bg-gray-50"
      on:click={toggleProductDropdown}
    >
      <div class="flex items-center flex-1">
        <div class="flex items-center gap-3">
          <div class="w-8 h-8 flex items-center justify-center bg-gray-100 rounded-lg">
            {currentProduct.icon}
          </div>
          <div>
            <div class="font-semibold">{currentProduct.name}</div>
          </div>
        </div>
      </div>
      <svg 
        class="w-5 h-5 text-gray-400 transform transition-transform duration-200" 
        class:rotate-180={isProductDropdownOpen}
        viewBox="0 0 20 20" 
        fill="currentColor"
      >
        <path fill-rule="evenodd" d="M5.293 7.293a1 1 0 011.414 0L10 10.586l3.293-3.293a1 1 0 111.414 1.414l-4 4a1 1 0 01-1.414 0l-4-4a1 1 0 010-1.414z" clip-rule="evenodd" />
      </svg>
    </button>

    {#if isProductDropdownOpen}
      <div 
        class="absolute top-full left-0 right-0 bg-white border-b border-gray-200 shadow-lg z-50"
      >
        <div class="p-4">
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
                    <div class="w-8 h-8 flex items-center justify-center bg-gray-100 rounded-lg">
                      {product.icon}
                    </div>
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
                <div class="w-8 h-8 flex items-center justify-center bg-gray-100 rounded-lg">
                  +
                </div>
                <span>Add product</span>
              </button>
            </li>
          </ul>
        </div>
      </div>
    {/if}
  </div>
</header> 