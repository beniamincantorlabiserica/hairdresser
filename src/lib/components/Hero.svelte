
<script>
  import { onMount } from 'svelte';
  import { fade, fly } from 'svelte/transition';
  import img from "$lib/images/main3.jpg";
  
  let visible = false;
  
  onMount(() => {
    // Trigger animations after component mounts
    setTimeout(() => {
      visible = true;
    }, 100);
  });
</script>

<div class="relative w-full overflow-hidden" style="height: 100vh; min-height: 500px; max-height: 900px;">
  <!-- Background image with overlay -->
  <div class="absolute inset-0 z-0">
    <img
      src={img}
      alt="Stylish salon background"
      class="h-full w-full object-cover"
    />
    <div class="absolute inset-0 bg-black/40"></div>
  </div>

  <!-- Content container -->
  <div class="relative z-10 flex h-full flex-col items-center justify-center px-4 text-center text-white">
    {#if visible}
      <div in:fly={{ y: 50, duration: 1000, delay: 200 }}>
        <h2 class="mb-2 font-serif text-xl font-light uppercase tracking-wider sm:text-2xl md:text-3xl">Welcome to</h2>
      </div>
      
      <div in:fly={{ y: 50, duration: 1000, delay: 400 }}>
        <h1 class="mb-4 font-serif text-4xl font-bold uppercase tracking-wide sm:text-5xl md:text-6xl lg:text-7xl">Elegance</h1>
      </div>
      
      <div in:fly={{ y: 50, duration: 1000, delay: 600 }}>
        <p class="mb-8 max-w-md text-base sm:text-lg md:text-xl">Where style meets confidence. Your journey to beautiful hair begins here.</p>
      </div>
      
      <div in:fade={{ duration: 1000, delay: 800 }} class="flex flex-col space-y-4 sm:flex-row sm:space-y-0 sm:space-x-4">
        <button class="group relative overflow-hidden rounded-full border-2 border-white bg-transparent px-6 py-3 font-medium uppercase tracking-wider text-white transition duration-300 hover:bg-white hover:text-black">
          Book Now
          <span class="absolute bottom-0 left-0 h-1 w-0 bg-white transition-all duration-300 group-hover:w-full"></span>
        </button>
        
        <button class="group relative overflow-hidden rounded-full bg-white px-6 py-3 font-medium uppercase tracking-wider text-black transition duration-300 hover:bg-transparent hover:text-white" on:click={() => window.scrollTo({ top: document.getElementById('services').offsetTop, behavior: 'smooth' })}>
          Our Services
          <span class="absolute bottom-0 left-0 h-1 w-0 bg-white transition-all duration-300 group-hover:w-full"></span>
        </button>
      </div>
    {/if}
  </div>
</div>