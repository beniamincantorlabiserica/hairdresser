<!-- SalonGallery.svelte -->
<script>
    import { onMount } from 'svelte';
    import { fade, fly } from 'svelte/transition';
    import img from "$lib/images/img3.jpg"; 
    import bg from "$lib/images/bg.jpg";
    import insta from "$lib/images/insta.png";
    import { goto } from '$app/navigation';
    
    let visible = false;
    
    onMount(() => {
      // Create an intersection observer to trigger animations when section is in view
      const observer = new IntersectionObserver((entries) => {
        if (entries[0].isIntersecting) {
          visible = true;
          observer.disconnect();
        }
      }, { threshold: 0.2 });
      
      const section = document.getElementById('gallery-section');
      if (section) observer.observe(section);
      
      return () => {
        if (section) observer.unobserve(section);
      };
    });
  </script>
  
  <section id="gallery-section" class="relative overflow-hidden bg-[#6D6559] py-24">
    <!-- Background decorative elements - curved lines in top left -->
    <div class="absolute left-0 top-0 h-64 w-64 opacity-20">
      <svg viewBox="0 0 200 200" xmlns="http://www.w3.org/2000/svg">
        <path d="M40,10 Q70,10 70,40 T40,70 T10,40 T40,10" fill="none" stroke="#fff" stroke-width="2"/>
        <path d="M50,20 Q80,20 80,50 T50,80 T20,50 T50,20" fill="none" stroke="#d18484" stroke-width="2"/>
        <path d="M60,30 Q90,30 90,60 T60,90 T30,60 T60,30" fill="none" stroke="#fff" stroke-width="2"/>
        <path d="M70,40 Q100,40 100,70 T70,100 T40,70 T70,40" fill="none" stroke="#d18484" stroke-width="2"/>
      </svg>
    </div>
    
    <!-- Large leaf decoration (right side) -->
    <div class="absolute bottom-0 right-0 z-0 h-full w-1/2 overflow-hidden">
      <!-- <img 
        src={bg}
        alt="Decorative monstera leaf" 
        class="absolute -right-24 -bottom-10 z-0 h-auto w-full max-w-3xl transform object-contain"
      /> -->
    </div>
    
    <!-- Main content container -->
    <div class="container relative z-10 mx-auto px-6 md:px-12">
      <div class="grid grid-cols-1 items-center gap-12 md:grid-cols-2">
        <!-- Left side content -->
        <div class="z-10">
          {#if visible}
            <div in:fly={{ y: 20, duration: 800, delay: 300 }} class="mb-6">
              <h2 class="font-serif text-4xl font-bold text-white md:text-5xl lg:text-6xl">
                We get better every day thru training and hard work
              </h2>
            </div>
            
            <div in:fade={{ duration: 800, delay: 500 }} class="mb-12 text-white opacity-90">
              <p>
                Ut ultricies imperdiet sodales. Aliquam fringilla aliquam ex sit amet elementum. Proin bibendum sollicitudin feugiat. 
                Curabitur ut egestas justo, vitae molestie ante. Integer magna purus, commodo in diam nec, pretium auctor sapien.
              </p>
            </div>
            
            <div in:fade={{ duration: 800, delay: 700 }}>
              <button class="bg-red-300 bg-opacity-60 px-8 py-3 font-medium uppercase tracking-wider text-white transition duration-300 hover:bg-opacity-80" on:click={() => goto('/gallery')}>
                See Gallery
              </button>
            </div>
          {/if}
        </div>
        
        <!-- Right side content - Instagram gallery teaser -->
        <div class="relative z-10">
          {#if visible}
            <div in:fade={{ duration: 1000, delay: 400 }} class="relative">
              <!-- Main haircut image -->
              <div class="relative mx-auto max-w-sm">
                <img 
                  src={img}
                  alt="Hairstylist cutting client's hair" 
                  class="w-full rounded-md shadow-lg"
                />
              </div>
              
              <!-- Instagram Card -->
              <div in:fly={{ x: 30, y: 30, duration: 800, delay: 600 }} class="absolute -bottom-12 -right-12 bg-white p-6 shadow-xl md:max-w-xs">
                <a href="https://www.instagram.com" target="_blank">
                    <div class="mb-5 flex items-center">
                    <img 
                        src={insta}
                        alt="Instagram icon" 
                        class="mr-3 h-8 w-8 rounded-md opacity-70"
                    />
                    </div>

                    <h3 class="mb-1 text-lg font-bold uppercase text-gray-900">See the gallery</h3>
                    <p class="mb-3 text-sm uppercase text-gray-900">on Instagram</p>
                    
                    <div class="mt-4">
                    <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 text-red-400" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M14 5l7 7m0 0l-7 7m7-7H3" />
                    </svg>
                    </div>
                </a>
              </div>
            </div>
          {/if}
        </div>
      </div>
    </div>
  </section>