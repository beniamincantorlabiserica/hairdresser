<!-- PremiumServices.svelte -->
<script>
    import { onMount } from 'svelte';
    import { fade, fly } from 'svelte/transition';
    import service1 from "$lib/images/service.jpeg";
    import service2 from "$lib/images/service2.jpg";
    import service3 from "$lib/images/service3.jpg";
    import service4 from "$lib/images/service4.webp";



    let visible = false;
    
    // Services data
    const services = [
      {
        id: 1,
        name: "Hair styling",
        price: "From 1300 DKK",
        image: service1
      },
      {
        id: 2,
        name: "Wedding service",
        price: "From 1500 DKK",
        image: service2
      },
      {
        id: 3,
        name: "Manly haircut",
        price: "From 250 DKK",
        image: service3
      },
      {
        id: 4,
        name: "Beard trimming",
        price: "From 120 DKK",
        image: service4
      }
    ];
    
    onMount(() => {
      // Create an intersection observer to trigger animations when section is in view
      const observer = new IntersectionObserver((entries) => {
        if (entries[0].isIntersecting) {
          visible = true;
          observer.disconnect();
        }
      }, { threshold: 0.1 });
      
      const section = document.getElementById('services-section');
      if (section) observer.observe(section);
      
      return () => {
        if (section) observer.unobserve(section);
      };
    });
  </script>
  
  <section id="services-section" class="relative overflow-hidden bg-slate-800 py-24">
    <!-- Background subtle curved lines -->
    <div class="absolute inset-0 z-0 opacity-10">
      <svg width="100%" height="100%" xmlns="http://www.w3.org/2000/svg">
        <path d="M0,100 C150,200 350,0 500,100 C650,200 850,0 1000,100 C1150,200 1350,0 1500,100" stroke="white" stroke-width="3" fill="none" />
        <path d="M0,250 C150,350 350,150 500,250 C650,350 850,150 1000,250 C1150,350 1350,150 1500,250" stroke="white" stroke-width="3" fill="none" />
        <path d="M0,400 C150,500 350,300 500,400 C650,500 850,300 1000,400 C1150,500 1350,300 1500,400" stroke="white" stroke-width="3" fill="none" />
      </svg>
    </div>

    
    <div class="container relative z-10 mx-auto px-6 md:px-12">
      <!-- Section header -->
      {#if visible}
        <div class="mb-6 text-center" in:fade={{ duration: 800 }}>
          <p class="text-sm font-medium uppercase tracking-widest text-red-300">What can we do for you</p>
        </div>
        
        <div class="mb-16 text-center" in:fade={{ duration: 800, delay: 200 }}>
          <h2 class="font-serif text-4xl font-bold text-white md:text-5xl">
            Check out our premium services
          </h2>
        </div>
      {/if}
      
      <!-- Services grid -->
      <div class="grid grid-cols-1 gap-6 sm:grid-cols-2 lg:grid-cols-4">
        {#each services as service, i}
          {#if visible}
            <div 
              in:fly={{ y: 30, duration: 800, delay: 200 + (i * 100) }}
              class="group relative overflow-hidden rounded-sm transition-transform duration-300 hover:translate-y-[-5px]"
            >
              <!-- Service Image -->
              <div class="relative h-96 overflow-hidden sm:h-80 md:h-72">
                <img 
                  src={service.image} 
                  alt={service.name} 
                  class="h-full w-full object-cover transition-transform duration-500 group-hover:scale-110"
                />
                
                <!-- Price Tag -->
                <div class="absolute top-4 right-4 rounded-sm bg-red-300 px-3 py-1 text-sm font-medium text-white">
                  {service.price}
                </div>
                
                <!-- Service name -->
                <div class="absolute bottom-0 left-0 right-0 bg-gradient-to-t from-black to-transparent p-6 pt-12">
                  <h3 class="text-xl font-bold text-white">{service.name}</h3>
                  
                  <!-- Underline decoration for the active/last service -->
                  {#if i === 3}
                    <div class="mt-2 h-0.5 w-24 bg-white"></div>
                  {/if}
                </div>
              </div>
            </div>
          {/if}
        {/each}
      </div>
    </div>
  </section>