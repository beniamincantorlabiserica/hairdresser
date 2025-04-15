<!-- AboutUs.svelte -->
<script>
  import { onMount } from 'svelte';
  import { fade, fly } from 'svelte/transition';
  import img from "$lib/images/img.jpg";
  let visible = false;
  
  // Add a variable to control the vertical position of the "About Us" text
  // Negative value moves it up, positive value moves it down
  let aboutUsTextPosition = -120; // Starting position (px)
  
  onMount(() => {
    // Create an intersection observer to trigger animations when section is in view
    const observer = new IntersectionObserver((entries) => {
      if (entries[0].isIntersecting) {
        visible = true;
        observer.disconnect();
      }
    }, { threshold: 0.2 });
    
    const section = document.getElementById('about-section');
    if (section) observer.observe(section);
    
    return () => {
      if (section) observer.unobserve(section);
    };
  });
</script>

<section id="about-section" class="relative  bg-white py-[10%] mt-36">
  <!-- Moved "About Us" Watermark to the top with adjustable position -->
  <div class="absolute inset-x-0 top-0 z-0 flex items-start justify-center overflow-hidden">
    <h1 
      class="font-serif text-[180px] font-bold text-gray-200 md:text-[240px] lg:text-[300px]"
      style="transform: translateY({aboutUsTextPosition}px);"
    >About Us</h1>
  </div>
  
  <div class="container relative z-10 mx-auto px-6 md:px-12">
    <div class="flex flex-col items-center gap-12 md:flex-row md:items-start md:gap-16 lg:gap-24">
      <!-- Left Column - Image with vertical line -->
      <div class="relative w-full md:w-5/12">
        {#if visible}
          <div in:fade={{ duration: 800, delay: 200 }} class="relative">
            <img 
              src={img} 
              alt="Hairstylist model with beautiful hair" 
              class="w-full rounded-md shadow-xl"
            />
            
            <!-- Decorative vertical line -->
            <div 
              in:fly={{ y: 100, duration: 1000, delay: 600 }} 
              class="absolute -bottom-12 left-1/2 h-24 w-0.5 -translate-x-1/2 bg-red-300 md:left-1/2 md:h-32"
            ></div>
          </div>
        {/if}
      </div>
      
      <!-- Right Column - Text Content -->
      <div class="w-full md:w-7/12">
        {#if visible}
          <div in:fly={{ x: 20, duration: 800, delay: 300 }} class="mb-6">
            <h2 class="font-serif text-4xl font-bold text-slate-800 md:text-5xl">
              Let your hair do the talking
            </h2>
          </div>
          
          <div in:fly={{ x: 20, duration: 800, delay: 500 }} class="space-y-4 text-slate-600">
            <p>
              Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla mauris dolor, gravida a varius blandit, auctor eget purus. Phasellus scelerisque sapien sit amet mauris laoreet, eget scelerisque nunc cursus. Duis ultricies malesuada leo vel aliquet. Curabitur rutrum porta dui eget mollis. Nullam lacinia dictum auctor.
            </p>
            
            <p>
              Class aptent taciti sociosqu ad litora torquent per conubia nostra, per inceptos himenaeos. Orci varius natoque penatibus et magnis dis parturient montes.
            </p>
            
            <div in:fade={{ duration: 800, delay: 800 }} class="mt-8">
              <button class="group relative inline-flex items-center overflow-hidden rounded-full border-2 border-slate-800 bg-transparent px-6 py-3 font-medium text-slate-800 transition duration-300 hover:bg-slate-800 hover:text-white">
                <span>Read More About Our Story</span>
                <svg xmlns="http://www.w3.org/2000/svg" class="ml-2 h-5 w-5" viewBox="0 0 20 20" fill="currentColor">
                  <path fill-rule="evenodd" d="M12.293 5.293a1 1 0 011.414 0l4 4a1 1 0 010 1.414l-4 4a1 1 0 01-1.414-1.414L14.586 11H3a1 1 0 110-2h11.586l-2.293-2.293a1 1 0 010-1.414z" clip-rule="evenodd" />
                </svg>
                <span class="absolute bottom-0 left-0 h-1 w-0 bg-slate-800 transition-all duration-300 group-hover:w-full"></span>
              </button>
            </div>
          </div>
        {/if}
      </div>
    </div>
  </div>
</section>