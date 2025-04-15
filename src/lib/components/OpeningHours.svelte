<!-- OpeningTimes.svelte -->
<script>
    import { onMount } from 'svelte';
    import { fade, fly } from 'svelte/transition';
    import img from "$lib/images/openinghours.webp"; 


    let visible = false;
    
    // Opening hours data
    const openingHours = [
      { day: "Monday", hours: "9:00 AM - 7:00 PM" },
      { day: "Tuesday", hours: "9:00 AM - 7:00 PM" },
      { day: "Wednesday", hours: "9:00 AM - 7:00 PM" },
      { day: "Thursday", hours: "9:00 AM - 8:00 PM" },
      { day: "Friday", hours: "9:00 AM - 8:00 PM" },
      { day: "Saturday", hours: "9:00 AM - 6:00 PM" },
      { day: "Sunday", hours: "Closed" }
    ];
    
    onMount(() => {
      // Create an intersection observer to trigger animations when section is in view
      const observer = new IntersectionObserver((entries) => {
        if (entries[0].isIntersecting) {
          visible = true;
          observer.disconnect();
        }
      }, { threshold: 0.2 });
      
      const section = document.getElementById('opening-times-section');
      if (section) observer.observe(section);
      
      return () => {
        if (section) observer.unobserve(section);
      };
    });
  </script>
  
  <section id="opening-times-section" class="relative overflow-hidden bg-white py-16 sm:py-20 md:py-24">
    <!-- Background decorative elements - subtle curved lines -->
    <div class="absolute right-0 top-0 h-64 w-64 opacity-10">
      <svg viewBox="0 0 200 200" xmlns="http://www.w3.org/2000/svg">
        <path d="M40,10 Q70,10 70,40 T40,70 T10,40 T40,10" fill="none" stroke="#333" stroke-width="2"/>
        <path d="M50,20 Q80,20 80,50 T50,80 T20,50 T50,20" fill="none" stroke="#333" stroke-width="2"/>
        <path d="M60,30 Q90,30 90,60 T60,90 T30,60 T60,30" fill="none" stroke="#333" stroke-width="2"/>
        <path d="M70,40 Q100,40 100,70 T70,100 T40,70 T70,40" fill="none" stroke="#333" stroke-width="2"/>
      </svg>
    </div>
    
    <!-- Main content container -->
    <div class="container relative z-10 mx-auto px-4 sm:px-6 md:px-12">
      <div class="grid grid-cols-1 items-center gap-10 sm:gap-12 md:grid-cols-2">
        <!-- Left side - opening hours -->
        <div class="z-10">
          {#if visible}
            <div in:fade={{ duration: 800 }} class="mb-3 sm:mb-4">
              <p class="text-sm font-medium uppercase tracking-widest text-red-400">Visit our salon</p>
            </div>
            
            <div in:fly={{ y: 20, duration: 800, delay: 200 }} class="mb-4 sm:mb-6 md:mb-8">
              <h2 class="font-serif text-3xl font-bold text-slate-800 sm:text-4xl md:text-5xl">
                Opening Hours
              </h2>
            </div>
            
            <div in:fly={{ y: 20, duration: 800, delay: 300 }} class="mb-6 max-w-md sm:mb-8">
              <p class="text-slate-600">
                We are ready to pamper you during our business hours. Walk-ins are welcome,
                but appointments are recommended for guaranteed service.
              </p>
            </div>
            
            <div in:fly={{ y: 20, duration: 800, delay: 400 }} class="space-y-3 sm:space-y-4">
              {#each openingHours as { day, hours }, i}
                <div class="flex justify-between border-b border-slate-200 pb-2">
                  <div class="font-medium text-slate-900">{day}</div>
                  <div class="text-right text-slate-700">{hours}</div>
                </div>
              {/each}
            </div>
            
            <div in:fade={{ duration: 800, delay: 800 }} class="mt-8 sm:mt-10">
              <button class="group relative inline-flex items-center overflow-hidden rounded-full border-2 border-red-400 bg-transparent px-5 py-2 sm:px-6 sm:py-3 font-medium text-red-500 transition duration-300 hover:bg-red-400 hover:text-white w-full justify-center sm:w-auto">
                <span>Book Appointment</span>
                <svg xmlns="http://www.w3.org/2000/svg" class="ml-2 h-5 w-5" viewBox="0 0 20 20" fill="currentColor">
                  <path fill-rule="evenodd" d="M12.293 5.293a1 1 0 011.414 0l4 4a1 1 0 010 1.414l-4 4a1 1 0 01-1.414-1.414L14.586 11H3a1 1 0 110-2h11.586l-2.293-2.293a1 1 0 010-1.414z" clip-rule="evenodd" />
                </svg>
                <span class="absolute bottom-0 left-0 h-1 w-0 bg-red-400 transition-all duration-300 group-hover:w-full"></span>
              </button>
            </div>
          {/if}
        </div>
        
        <!-- Right side - image and contact details card -->
        <div class="relative mt-8 md:mt-0">
          {#if visible}
            <div in:fade={{ duration: 1000, delay: 300 }} class="relative">
              <!-- Main salon image -->
              <img 
                src={img}
                alt="Salon interior" 
                class="w-full rounded-md object-cover shadow-xl h-[300px] sm:h-[400px] md:h-[500px] lg:h-[550px]"
              />
              
              <!-- Contact info card - positioned differently on mobile vs desktop -->
              <div 
                in:fly={{ x: 30, y: 30, duration: 800, delay: 600 }} 
                class="w-full sm:max-w-sm md:absolute md:-bottom-12 md:-right-6 overflow-hidden rounded-md bg-white shadow-xl mt-6 md:mt-0"
              >
                <!-- Decorative top bar with gradient -->
                <div class="h-2 w-full bg-gradient-to-r from-red-300 to-red-500"></div>
                
                <div class="p-4 sm:p-6">
                  <h3 class="mb-4 sm:mb-5 text-xl font-bold text-slate-800">Contact Details</h3>
                  
                  <div class="space-y-3 sm:space-y-4">
                    <!-- Address with enhanced styling -->
                    <div class="group flex items-start rounded-md p-2 transition duration-300 hover:bg-red-50">
                      <div class="mr-3 sm:mr-4 flex h-8 w-8 sm:h-10 sm:w-10 items-center justify-center rounded-full bg-red-100 text-red-500 group-hover:bg-red-200 flex-shrink-0">
                        <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4 sm:h-5 sm:w-5" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M17.657 16.657L13.414 20.9a1.998 1.998 0 01-2.827 0l-4.244-4.243a8 8 0 1111.314 0z" />
                          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 11a3 3 0 11-6 0 3 3 0 016 0z" />
                        </svg>
                      </div>
                      <div>
                        <h4 class="text-xs sm:text-sm font-medium text-slate-500">Our Location</h4>
                        <p class="text-sm sm:text-base text-slate-700">123 Beauty Street, Salon City, SC 12345</p>
                      </div>
                    </div>
                    
                    <!-- Phone with enhanced styling -->
                    <div class="group flex items-start rounded-md p-2 transition duration-300 hover:bg-red-50">
                      <div class="mr-3 sm:mr-4 flex h-8 w-8 sm:h-10 sm:w-10 items-center justify-center rounded-full bg-red-100 text-red-500 group-hover:bg-red-200 flex-shrink-0">
                        <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4 sm:h-5 sm:w-5" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 5a2 2 0 012-2h3.28a1 1 0 01.948.684l1.498 4.493a1 1 0 01-.502 1.21l-2.257 1.13a11.042 11.042 0 005.516 5.516l1.13-2.257a1 1 0 011.21-.502l4.493 1.498a1 1 0 01.684.949V19a2 2 0 01-2 2h-1C9.716 21.002 3 14.286 3 8.001V5z" />
                        </svg>
                      </div>
                      <div>
                        <h4 class="text-xs sm:text-sm font-medium text-slate-500">Phone Number</h4>
                        <p class="text-sm sm:text-base text-slate-700">+1 (555) 123-4567</p>
                      </div>
                    </div>
                    
                    <!-- Email with enhanced styling -->
                    <div class="group flex items-start rounded-md p-2 transition duration-300 hover:bg-red-50">
                      <div class="mr-3 sm:mr-4 flex h-8 w-8 sm:h-10 sm:w-10 items-center justify-center rounded-full bg-red-100 text-red-500 group-hover:bg-red-200 flex-shrink-0">
                        <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4 sm:h-5 sm:w-5" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 8l7.89 5.26a2 2 0 002.22 0L21 8M5 19h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v10a2 2 0 002 2z" />
                        </svg>
                      </div>
                      <div>
                        <h4 class="text-xs sm:text-sm font-medium text-slate-500">Email Address</h4>
                        <p class="text-sm sm:text-base text-slate-700">info@yourbeautysalon.com</p>
                      </div>
                    </div>
                  </div>
                </div>
              </div>
            </div>
          {/if}
        </div>
      </div>
    </div>
  </section>