<script>
    import { onMount } from 'svelte';
    import { fade, fly, scale } from 'svelte/transition';
    import Header from "$lib/components/Header.svelte";
    import Footer from "$lib/components/Footer.svelte";
    
    // Import images - make sure these paths are correct
    import transformation1Before from "$lib/images/gallery/before.png";
    import transformation1After from "$lib/images/gallery/after.jpg";
    import transformation2Before from "$lib/images/gallery/before.png";
    import transformation2After from "$lib/images/gallery/after.jpg";
    import transformation3Before from "$lib/images/gallery/before.png";
    import transformation3After from "$lib/images/gallery/after.jpg";
    import transformation4Before from "$lib/images/gallery/before.png";
    import transformation4After from "$lib/images/gallery/after.jpg";
    import transformation5Before from "$lib/images/gallery/before.png";
    import transformation5After from "$lib/images/gallery/after.jpg";
    import transformation6Before from "$lib/images/gallery/before.png";
    import transformation6After from "$lib/images/gallery/after.jpg";
    
    // Gallery transformations data with dynamic information
    const transformations = [
      {
        id: 1,
        beforeImage: transformation1Before,
        afterImage: transformation1After,
        title: "Long to Short Bob",
        description: "A dramatic change from long locks to a stylish, modern bob that frames the face beautifully.",
        stylist: "Emma Johnson",
        time: "1.5 hours",
        services: ["Precision Cut", "Blow Dry Styling", "Hair Treatment"]
      },
      {
        id: 2,
        beforeImage: transformation2Before,
        afterImage: transformation2After,
        title: "Color Transformation",
        description: "From dark brunette to vibrant copper balayage with seamless blending and dimension.",
        stylist: "Michael Chen",
        time: "3 hours",
        services: ["Full Color", "Balayage Technique", "Toner Application", "Treatment Mask"]
      },
      {
        id: 3,
        beforeImage: transformation3Before,
        afterImage: transformation3After,
        title: "Curl Reconstruction",
        description: "Revitalizing natural curls with specialized treatments for enhanced definition and shine.",
        stylist: "Sophia Rodriguez",
        time: "2 hours",
        services: ["Curl Analysis", "Deep Conditioning", "Curl-Enhancing Cut", "Diffuse Drying"]
      },
      {
        id: 4,
        beforeImage: transformation4Before,
        afterImage: transformation4After,
        title: "Blonde Highlights",
        description: "Adding dimension with natural-looking blonde highlights that brighten the overall appearance.",
        stylist: "Emma Johnson",
        time: "2.5 hours",
        services: ["Foil Highlights", "Toner", "Gloss Treatment", "Blow Out"]
      },
      {
        id: 5,
        beforeImage: transformation5Before,
        afterImage: transformation5After,
        title: "Men's Style Upgrade",
        description: "A refined, modern cut that enhances natural features and provides easy daily styling.",
        stylist: "David Wilson",
        time: "45 minutes",
        services: ["Precision Cut", "Beard Trim", "Styling Tutorial"]
      },
      {
        id: 6,
        beforeImage: transformation6Before,
        afterImage: transformation6After,
        title: "Hair Extension Transformation",
        description: "Adding length and volume with premium hair extensions matched perfectly to natural color.",
        stylist: "Sophia Rodriguez",
        time: "4 hours",
        services: ["Extension Application", "Color Matching", "Blending Cut", "Styling"]
      }
    ];
    
    let visible = false;
    let selectedTransformation = null;
    let modalOpen = false;
    
    // Categories for filtering
    const categories = [
      { id: 'all', name: 'All' },
      { id: 'color', name: 'Color' },
      { id: 'cut', name: 'Cut' },
      { id: 'styling', name: 'Styling' }
    ];
    
    let activeCategory = 'all';
    
    function filterByCategory(category) {
      activeCategory = category;
      // In a real application, you would filter transformations based on categories
    }
    
    function openModal(transformation) {
      selectedTransformation = transformation;
      modalOpen = true;
      document.body.style.overflow = 'hidden'; // Prevent scrolling when modal is open
    }
    
    function closeModal() {
      modalOpen = false;
      document.body.style.overflow = ''; // Re-enable scrolling
    }
    
    // Close modal when clicking outside of it
    function handleModalBackgroundClick(event) {
      if (event.target === event.currentTarget) {
        closeModal();
      }
    }
    
    // Close modal with escape key
    function handleKeydown(event) {
      if (event.key === 'Escape' && modalOpen) {
        closeModal();
      }
    }
    
    onMount(() => {
      // Create an intersection observer to trigger animations when section is in view
      const observer = new IntersectionObserver((entries) => {
        if (entries[0].isIntersecting) {
          visible = true;
          observer.disconnect();
        }
      }, { threshold: 0.1 });
      
      const section = document.getElementById('gallery-section');
      if (section) observer.observe(section);
      
      return () => {
        if (section) observer.unobserve(section);
        document.body.style.overflow = ''; // Ensure scrolling is enabled when component unmounts
      };
    });
  </script>
  
  <svelte:window on:keydown={handleKeydown} />
  
  <Header />
  
  <main id="gallery-section" class="pt-8">
    <!-- Page Title Banner -->
    <div class="relative bg-slate-800 py-24 md:py-32">
      <div class="absolute inset-0 z-0 opacity-20">
        <svg width="100%" height="100%" xmlns="http://www.w3.org/2000/svg">
          <pattern id="pattern-circles" x="0" y="0" width="40" height="40" patternUnits="userSpaceOnUse" patternContentUnits="userSpaceOnUse">
            <circle cx="20" cy="20" r="3" fill="white" />
          </pattern>
          <rect x="0" y="0" width="100%" height="100%" fill="url(#pattern-circles)" />
        </svg>
      </div>
      
      <div class="container relative z-10 mx-auto px-6 text-center md:px-12">
        {#if visible}
          <div in:fade={{ duration: 800 }}>
            <h1 class="font-serif text-4xl font-bold text-white md:text-5xl lg:text-6xl">Transformation Gallery</h1>
            <p class="mx-auto mt-6 max-w-2xl text-lg text-slate-300">Browse our collection of stunning before and after transformations</p>
          </div>
        {/if}
      </div>
    </div>
    
    
    
    <!-- Gallery Grid Section -->
    <section class="py-12 md:py-16">
      <div class="container mx-auto px-6 md:px-12">
        <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
          {#each transformations as transformation, i}
            {#if visible}
              <div 
                in:fly={{ y: 20, duration: 800, delay: 200 + (i * 100) }} 
                class="group cursor-pointer rounded-md overflow-hidden shadow-md transition-transform duration-300 hover:-translate-y-2"
                on:click={() => openModal(transformation)}
                on:keypress={(e) => e.key === 'Enter' && openModal(transformation)}
                tabindex="0"
                role="button"
                aria-label={`View ${transformation.title} transformation`}
              >
                <div class="relative">
                  <!-- Before and After Side by Side -->
                  <div class="flex">
                    <!-- Before Image -->
                    <div class="w-1/2 relative">
                      <div class="absolute top-4 left-4 bg-slate-800 bg-opacity-70 text-white text-xs font-medium px-2 py-1 rounded-sm z-10">
                        BEFORE
                      </div>
                      <div class="h-64 sm:h-72 overflow-hidden">
                        <img src={transformation.beforeImage} alt={`${transformation.title} before`} class="w-full h-full object-cover" />
                      </div>
                    </div>
                    
                    <!-- After Image -->
                    <div class="w-1/2 relative">
                      <div class="absolute top-4 right-4 bg-red-400 bg-opacity-70 text-white text-xs font-medium px-2 py-1 rounded-sm z-10">
                        AFTER
                      </div>
                      <div class="h-64 sm:h-72 overflow-hidden">
                        <img src={transformation.afterImage} alt={`${transformation.title} after`} class="w-full h-full object-cover" />
                      </div>
                    </div>
                  </div>
                  
                  <!-- Overlay on hover -->
                  <div class="absolute inset-0 bg-black bg-opacity-30 opacity-0 transition-opacity duration-300 group-hover:opacity-100 flex items-center justify-center">
                    <span class="text-white font-medium px-4 py-2 rounded-full bg-red-400 bg-opacity-90">View Details</span>
                  </div>
                </div>
                
                <!-- Caption -->
                <div class="p-4 bg-white">
                  <h3 class="text-lg font-bold text-slate-800">{transformation.title}</h3>
                  <p class="text-sm text-slate-600 mt-1">{transformation.description}</p>
                </div>
              </div>
            {/if}
          {/each}
        </div>
      </div>
    </section>
    
    <!-- Testimonial Banner -->
    <section class="bg-red-400 bg-opacity-10 py-12 md:py-16">
      <div class="container mx-auto px-6 md:px-12 text-center">
        {#if visible}
          <div in:fade={{ duration: 800, delay: 400 }}>
            <blockquote class="max-w-3xl mx-auto text-xl md:text-2xl italic text-slate-700 font-serif">
              "The team at BeautySalon completely transformed my look in ways I never imagined possible. I've never felt more confident!"
            </blockquote>
            <p class="mt-4 text-slate-700 font-medium">— Sarah Johnson, Client</p>
          </div>
        {/if}
      </div>
    </section>
    
    <!-- Book Appointment CTA -->
    <section class="py-12 md:py-16 bg-slate-50">
      <div class="container mx-auto px-6 md:px-12 text-center">
        {#if visible}
          <div in:fade={{ duration: 800, delay: 200 }}>
            <h2 class="font-serif text-3xl font-bold text-slate-800 md:text-4xl">Ready for Your Transformation?</h2>
            <p class="mt-4 mx-auto max-w-2xl text-lg text-slate-600">Book your appointment today and let our expert stylists work their magic.</p>
            <div class="mt-8">
              <a 
                href="/booking" 
                class="inline-block rounded-full bg-red-400 px-8 py-3 font-medium uppercase tracking-wider text-white transition hover:bg-red-500"
              >
                Book Now
              </a>
            </div>
          </div>
        {/if}
      </div>
    </section>
    
    <!-- Modal for enlarged transformation view -->
    {#if modalOpen}
      <div 
        class="fixed inset-0 bg-black bg-opacity-75 z-50 flex items-center justify-center p-4 sm:p-6 md:p-8"
        on:click={handleModalBackgroundClick}
        in:fade={{ duration: 200 }}
      >
        <div 
          class="bg-white rounded-lg max-w-4xl w-full max-h-[90vh] overflow-auto"
          in:scale={{ start: 0.95, duration: 300 }}
        >
          <!-- Close button -->
          <div class="flex justify-end p-4">
            <button 
              class="text-slate-500 hover:text-slate-700"
              on:click={closeModal}
              aria-label="Close modal"
            >
              <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" />
              </svg>
            </button>
          </div>
          
          <!-- Modal content -->
          {#if selectedTransformation}
            <div class="p-4 sm:p-6">
              <h2 class="text-2xl font-bold text-slate-800 mb-4">{selectedTransformation.title}</h2>
              
              <!-- Before and After Images -->
              <div class="flex flex-col md:flex-row gap-6 mb-6">
                <!-- Before Image Column -->
                <div class="w-full md:w-1/2">
                  <div class="bg-slate-100 p-2 rounded-md">
                    <div class="mb-2 text-sm font-bold text-slate-700 uppercase">Before</div>
                    <div class="h-64 sm:h-80 rounded-md overflow-hidden">
                      <img src={selectedTransformation.beforeImage} alt={`${selectedTransformation.title} before`} class="w-full h-full object-cover" />
                    </div>
                  </div>
                </div>
                
                <!-- After Image Column -->
                <div class="w-full md:w-1/2">
                  <div class="bg-slate-100 p-2 rounded-md">
                    <div class="mb-2 text-sm font-bold text-slate-700 uppercase">After</div>
                    <div class="h-64 sm:h-80 rounded-md overflow-hidden">
                      <img src={selectedTransformation.afterImage} alt={`${selectedTransformation.title} after`} class="w-full h-full object-cover" />
                    </div>
                  </div>
                </div>
              </div>
              
              <!-- Description -->
              <div>
                <h3 class="text-lg font-bold text-slate-800 mb-2">About this Transformation</h3>
                <p class="text-slate-600">{selectedTransformation.description}</p>
                
                <!-- Additional details - now using dynamic data -->
                <div class="mt-4 pt-4 border-t border-slate-200">
                  <div class="grid grid-cols-2 gap-4">
                    <div>
                      <h4 class="text-sm font-bold text-slate-700">Services Used</h4>
                      <ul class="mt-1 list-disc pl-5 text-sm text-slate-600">
                        {#each selectedTransformation.services as service}
                          <li>{service}</li>
                        {/each}
                      </ul>
                    </div>
                    <div>
                      <h4 class="text-sm font-bold text-slate-700">Stylist</h4>
                      <p class="mt-1 text-sm text-slate-600">{selectedTransformation.stylist}</p>
                      
                      <h4 class="mt-3 text-sm font-bold text-slate-700">Time</h4>
                      <p class="mt-1 text-sm text-slate-600">{selectedTransformation.time}</p>
                    </div>
                  </div>
                </div>
              </div>
              
              <!-- Book Similar Service Button -->
              <div class="mt-6 text-center">
                <a 
                  href="/booking" 
                  class="inline-block rounded-full bg-red-400 px-6 py-2 font-medium text-white transition hover:bg-red-500"
                >
                  Book Similar Service
                </a>
              </div>
            </div>
          {/if}
        </div>
      </div>
    {/if}
  </main>
  
  <Footer />