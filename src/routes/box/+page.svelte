<script lang="ts">
  let messages = [
    { role: 'assistant', content: 'How can I help you today?' }
  ];
  let userInput = '';

  function handleSubmit() {
    if (userInput.trim()) {
      messages = [...messages, { role: 'user', content: userInput.trim() }];
      userInput = '';
      // Simulate AI response
      setTimeout(() => {
        messages = [...messages, { role: 'assistant', content: 'This is a simulated response.' }];
      }, 1000);
    }
  }
</script>

<div class="flex flex-col h-[calc(100vh-8rem)]">
  <!-- Chat messages container with auto scroll -->
  <div class="flex-1 overflow-y-auto px-4">
    <div class="max-w-3xl mx-auto">
      {#each messages as message}
        <div class="mb-6">
          <div class="flex items-start gap-4 {message.role === 'assistant' ? 'bg-gray-50' : ''} p-4 rounded-lg">
            <!-- Avatar -->
            <div class="w-8 h-8 rounded-full bg-gray-200 flex items-center justify-center flex-shrink-0">
              {#if message.role === 'assistant'}
                <svg class="w-5 h-5 text-gray-500" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                  <path d="M12 8v8m-4-4h8" stroke-linecap="round" />
                </svg>
              {:else}
                <svg class="w-5 h-5 text-gray-500" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                  <circle cx="12" cy="12" r="6" />
                  <circle cx="12" cy="10" r="2" />
                  <path d="M16 16c-1.5-2-4.5-2-8 0" />
                </svg>
              {/if}
            </div>
            <!-- Message content -->
            <div class="flex-1 prose max-w-none">
              <p class="text-gray-800">{message.content}</p>
            </div>
          </div>
        </div>
      {/each}
    </div>
  </div>

  <!-- Fixed input box at bottom -->
  <div class="border-t bg-white px-4 py-4">
    <div class="max-w-3xl mx-auto">
      <form 
        class="relative"
        on:submit|preventDefault={handleSubmit}
      >
        <input
          type="text"
          bind:value={userInput}
          placeholder="Send a message..."
          class="w-full p-4 pr-12 rounded-lg border border-gray-300 focus:outline-none focus:border-gray-400 focus:ring-0"
        />
        <button 
          type="submit"
          class="absolute right-2 top-1/2 -translate-y-1/2 p-2 text-gray-400 hover:text-gray-600"
          disabled={!userInput.trim()}
        >
          <svg class="w-6 h-6" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
            <path d="M5 12h14m-7-7l7 7-7 7" stroke-linecap="round" stroke-linejoin="round" />
          </svg>
        </button>
      </form>
    </div>
  </div>
</div> 