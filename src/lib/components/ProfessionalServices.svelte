<!-- ProfessionalService.svelte -->
<script>
    import { onMount } from 'svelte';
    import { fade, fly } from 'svelte/transition';
    import img from "$lib/images/img2.jpg"; 
    let visible = false;
    
    onMount(() => {
      // Create an intersection observer to trigger animations when section is in view
      const observer = new IntersectionObserver((entries) => {
        if (entries[0].isIntersecting) {
          visible = true;
          observer.disconnect();
        }
      }, { threshold: 0.2 });
      
      const section = document.getElementById('service-section');
      if (section) observer.observe(section);
      
      return () => {
        if (section) observer.unobserve(section);
      };
    });
  </script>
  
  <section id="service-section" class="relative overflow-hidden bg-white">
    <!-- Vertical "scroll down" text on the left -->
    <div class="absolute left-8 top-0 bottom-0 flex items-center">
      <div class="flex flex-col items-center">
        <div class="text-vertical transform rotate-180 text-xs font-medium tracking-widest text-slate-400" style="writing-mode: vertical-rl;">
          SCROLL DOWN
        </div>
        <div class="mt-3 h-16 w-px bg-red-400"></div>
      </div>
    </div>
    
    <!-- Main content container -->
    <div class="container mx-auto flex flex-col md:flex-row">
      <!-- Left side content -->
      <div class="w-full py-20 pl-20 pr-8 md:w-1/2 md:py-32">
        {#if visible}
          <div in:fade={{ duration: 800, delay: 200 }} class="mb-2">
            <p class="text-sm font-medium uppercase tracking-wide text-red-400">Professional service</p>
          </div>
          
          <div in:fly={{ y: 20, duration: 800, delay: 300 }} class="mb-12">
            <h2 class="font-serif text-4xl font-bold text-slate-800 md:text-5xl">
              This is what you get
            </h2>
          </div>
          
          <div in:fly={{ y: 20, duration: 800, delay: 400 }} class="space-y-6">
            <!-- Service list items -->
            <div class="flex items-start border-b border-gray-200 pb-4">
              <svg xmlns="http://www.w3.org/2000/svg" class="mr-3 h-5 w-5 flex-shrink-0 text-green-500" viewBox="0 0 20 20" fill="currentColor">
                <path fill-rule="evenodd" d="M16.707 5.293a1 1 0 010 1.414l-8 8a1 1 0 01-1.414 0l-4-4a1 1 0 011.414-1.414L8 12.586l7.293-7.293a1 1 0 011.414 0z" clip-rule="evenodd" />
              </svg>
              <p class="text-slate-600">Lorem ipsum dolor sit amet, consectetur</p>
            </div>
            
            <div class="flex items-start border-b border-gray-200 pb-4">
              <svg xmlns="http://www.w3.org/2000/svg" class="mr-3 h-5 w-5 flex-shrink-0 text-green-500" viewBox="0 0 20 20" fill="currentColor">
                <path fill-rule="evenodd" d="M16.707 5.293a1 1 0 010 1.414l-8 8a1 1 0 01-1.414 0l-4-4a1 1 0 011.414-1.414L8 12.586l7.293-7.293a1 1 0 011.414 0z" clip-rule="evenodd" />
              </svg>
              <p class="text-slate-600">Adipisicing elit, sed do eiusmod tempor</p>
            </div>
            
            <div class="flex items-start border-b border-gray-200 pb-4">
              <svg xmlns="http://www.w3.org/2000/svg" class="mr-3 h-5 w-5 flex-shrink-0 text-green-500" viewBox="0 0 20 20" fill="currentColor">
                <path fill-rule="evenodd" d="M16.707 5.293a1 1 0 010 1.414l-8 8a1 1 0 01-1.414 0l-4-4a1 1 0 011.414-1.414L8 12.586l7.293-7.293a1 1 0 011.414 0z" clip-rule="evenodd" />
              </svg>
              <p class="text-slate-600">Incididunt ut labore et dolore magna aliqua.</p>
            </div>
            
            <div class="flex items-start border-b border-gray-200 pb-4">
              <svg xmlns="http://www.w3.org/2000/svg" class="mr-3 h-5 w-5 flex-shrink-0 text-green-500" viewBox="0 0 20 20" fill="currentColor">
                <path fill-rule="evenodd" d="M16.707 5.293a1 1 0 010 1.414l-8 8a1 1 0 01-1.414 0l-4-4a1 1 0 011.414-1.414L8 12.586l7.293-7.293a1 1 0 011.414 0z" clip-rule="evenodd" />
              </svg>
              <p class="text-slate-600">Exercitation ullamco laboris nisi ut aliquip</p>
            </div>
          </div>
        {/if}
      </div>
      
      <!-- Right side image -->
      <div class="relative w-full md:w-1/2">
        {#if visible}
          <div in:fade={{ duration: 1000, delay: 200 }} class="h-full">
            <img 
              src={img}
              alt="Professional hairstylist cutting client's hair" 
              class="h-full w-full object-cover"
            />
          </div>
        {/if}
      </div>
    </div>
  </section>