<script lang="ts">
  let activeTab = 'Core';
  let productName = '';
  let productType = '';
  let productDescription = '';

  function setActiveTab(tab: string) {
    activeTab = tab;
  }
</script>

<div class="products-container">
  <div class="products-content">
    <div class="tabs">
      <button class:active={activeTab === 'Core'} on:click={() => setActiveTab('Core')}>Core</button>
      <button class:active={activeTab === 'Options'} on:click={() => setActiveTab('Options')}>Options</button>
      <button class:active={activeTab === 'Properties'} on:click={() => setActiveTab('Properties')}>Properties</button>
    </div>

    <div class="tab-content">
      {#if activeTab === 'Core'}
        <div>
          <table class="notion-table">
            <tbody>
              <tr>
                <td>Name</td>
                <td><input type="text" bind:value={productName} class="notion-input" /></td>
              </tr>
              <tr>
                <td>Type</td>
                <td><input type="text" bind:value={productType} class="notion-input" /></td>
              </tr>
              <tr>
                <td>Description</td>
                <td><input type="text" bind:value={productDescription} class="notion-input" /></td>
              </tr>
            </tbody>
          </table>
        </div>
      {:else if (activeTab === 'Options')}
        <div>Content for Options tab</div>
      {:else if (activeTab === 'Properties')}
        <div>Content for Properties tab</div>
      {/if}
    </div>
  </div>
</div>

<style>
  .products-container {
    padding: 1rem;
  }

  .products-content {
    margin-top: 0;
  }

  .tabs {
    display: flex;
    /* margin-bottom: 1rem; */
    border-bottom: 1px solid #eee;
  }

  .tabs button {
    padding: 0.3rem 0.75rem;
    border: none;
    background-color: transparent;
    cursor: pointer;
    color: #777;
    margin-right: 0.75rem;
    font-size: 0.85rem;
    transition: color 0.3s ease;
  }

  .tabs button.active {
    color: #333;
    border-bottom: 2px solid #333;
  }

  .tab-content {
    padding: 0rem;
  }

  .notion-table {
    width: 100%;
    border-collapse: collapse;
    font-size: 0.85rem;
  }

  .notion-table td {
    border-bottom: 1px solid #eee;
    padding: 0.4rem 0.5rem;
    text-align: left;
  }

  .notion-table td:first-child {
    color: #555;
    width: 30%;
  }

  .notion-input {
    width: 100%;
    border: none;
    padding: 0.4rem 0.5rem;
    font-size: inherit;
    font-family: inherit;
    outline: none;
    background-color: transparent;
  }
</style> 