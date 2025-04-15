<script>
    import { onMount } from 'svelte';
    import { fade, fly } from 'svelte/transition';
    import Header from "$lib/components/Header.svelte";
    import Footer from "$lib/components/Footer.svelte";
    import aboutTeamImage from "$lib/images/main.jpg"; // You'll need to add this image to your project
    import person from "$lib/images/person.jpg"; 
    import bg from "$lib/images/Media.jpeg"; 


    let visible = false;
    let formData = {
      name: '',
      email: '',
      phone: '',
      message: ''
    };
    let formSubmitted = false;
    let formError = false;
    
    function handleSubmit() {
      // In a real application, you would send the form data to a server
      // For demo purposes, we'll just simulate a successful submission
      if (formData.name && formData.email && formData.message) {
        formSubmitted = true;
        formError = false;
      } else {
        formError = true;
      }
    }
    
    onMount(() => {
      // Create an intersection observer to trigger animations when section is in view
      const observer = new IntersectionObserver((entries) => {
        if (entries[0].isIntersecting) {
          visible = true;
          observer.disconnect();
        }
      }, { threshold: 0.2 });
      
      const section = document.getElementById('about-page-section');
      if (section) observer.observe(section);
      
      return () => {
        if (section) observer.unobserve(section);
      };
    });
  </script>
  
  <Header />
  
  <main id="about-page-section" class="pt-8">
    <!-- Page Title Banner with increased padding -->
    <div class="relative bg-slate-800 py-24 md:py-32">
      <div class="absolute inset-0 z-0 opacity-90">
        <!-- <svg width="100%" height="100%" xmlns="http://www.w3.org/2000/svg">
          <pattern id="pattern-circles" x="0" y="0" width="40" height="40" patternUnits="userSpaceOnUse" patternContentUnits="userSpaceOnUse">
            <circle cx="20" cy="20" r="3" fill="white" />
          </pattern>
          <rect x="0" y="0" width="100%" height="100%" fill="url(#pattern-circles)" />
        </svg> -->
        <img
          src={bg}
          alt="Decorative background"
          class="absolute inset-0 h-full w-full object-cover opacity-40"
        />
      </div>
      
      <div class="container relative z-10 mx-auto px-6 text-center md:px-12">
        {#if visible}
          <div in:fade={{ duration: 800 }}>
            <h1 class="font-serif text-4xl font-bold text-white md:text-5xl lg:text-6xl">About Our Salon</h1>
            <p class="mx-auto mt-6 max-w-2xl text-lg text-slate-300">Get to know our story and passion for beauty</p>
          </div>
        {/if}
      </div>
    </div>
    
    <!-- Contact Form Section -->
    <section class="py-12 md:py-16">
      <div class="container mx-auto px-6 md:px-12">
        {#if visible}
          <div in:fly={{ y: 30, duration: 800, delay: 300 }} class="max-w-3xl mx-auto rounded-md bg-slate-50 p-8 shadow-md">
            <h3 class="mb-6 text-center font-serif text-2xl font-bold text-slate-800">Get In Touch</h3>
            
            {#if formSubmitted}
              <div class="rounded-md bg-green-100 p-4 text-center text-green-800">
                <p class="font-medium">Thank you for your message!</p>
                <p class="mt-2">We'll get back to you as soon as possible.</p>
              </div>
            {:else}
              <form on:submit|preventDefault={handleSubmit} class="space-y-4">
                <div class="grid grid-cols-1 gap-4 md:grid-cols-2">
                  <div>
                    <label for="name" class="mb-1 block text-sm font-medium text-slate-700">Full Name*</label>
                    <input 
                      type="text" 
                      id="name" 
                      bind:value={formData.name} 
                      class="w-full rounded-md border border-slate-300 px-4 py-2 focus:border-red-400 focus:outline-none focus:ring-red-400"
                      required
                    />
                  </div>
                  
                  <div>
                    <label for="email" class="mb-1 block text-sm font-medium text-slate-700">Email Address*</label>
                    <input 
                      type="email" 
                      id="email" 
                      bind:value={formData.email} 
                      class="w-full rounded-md border border-slate-300 px-4 py-2 focus:border-red-400 focus:outline-none focus:ring-red-400"
                      required
                    />
                  </div>
                </div>
                
                <div>
                  <label for="phone" class="mb-1 block text-sm font-medium text-slate-700">Phone Number</label>
                  <input 
                    type="tel" 
                    id="phone" 
                    bind:value={formData.phone} 
                    class="w-full rounded-md border border-slate-300 px-4 py-2 focus:border-red-400 focus:outline-none focus:ring-red-400"
                  />
                </div>
                
                <div>
                  <label for="message" class="mb-1 block text-sm font-medium text-slate-700">Your Message*</label>
                  <textarea 
                    id="message" 
                    bind:value={formData.message} 
                    rows="4" 
                    class="w-full rounded-md border border-slate-300 px-4 py-2 focus:border-red-400 focus:outline-none focus:ring-red-400"
                    required
                  ></textarea>
                </div>
                
                {#if formError}
                  <div class="text-sm text-red-500">
                    Please fill out all required fields.
                  </div>
                {/if}
                
                <button 
                  type="submit" 
                  class="w-full rounded-full bg-red-400 px-6 py-3 text-center font-medium uppercase tracking-wider text-white transition hover:bg-red-500"
                >
                  Send Message
                </button>
              </form>
            {/if}
          </div>
        {/if}
      </div>
    </section>
    
    <!-- Compressed About Content Section with image left, text right -->
    <section class="py-12 md:py-16 bg-slate-50">
      <div class="container mx-auto px-6 md:px-12">
        {#if visible}
          <div class="flex flex-col md:flex-row gap-8 md:gap-12 items-center">
            <!-- Left side - Image -->
            <div class="w-full md:w-1/2">
              <div in:fade={{ duration: 1000, delay: 200 }} class="relative">
                <div class="relative overflow-hidden rounded-md shadow-xl">
                  <img 
                    src={aboutTeamImage} 
                    alt="Our salon interior" 
                    class="w-full object-cover h-full"
                  />
                  
                  <!-- Decorative elements -->
                  <div class="absolute -left-4 -top-4 h-16 w-16 rounded-full border-8 border-red-300 bg-white opacity-80"></div>
                  <div class="absolute -bottom-4 -right-4 h-16 w-16 rounded-full border-8 border-red-300 bg-white opacity-80"></div>
                </div>
              </div>
            </div>
            
            <!-- Right side - Condensed text content -->
            <div class="w-full md:w-1/2 md:mt-12">
              <div in:fly={{ y: 20, duration: 800, delay: 300 }} class="bg-white p-8 rounded-md shadow-md -mt-8 md:mt-16 md:-ml-16 z-10 relative">
                <h2 class="mb-4 font-serif text-3xl font-bold text-slate-800">Our Story</h2>
                <div class="text-slate-600">
                  <p class="mb-4">
                    Founded in 2015, BeautySalon has grown from a small local studio to one of the most respected beauty establishments in the area. Our journey began with a simple vision: to create a space where clients feel truly valued.
                  </p>
                  <p class="mb-4">
                    What sets us apart is our commitment to continuous education and staying at the forefront of industry trends. We use only premium products that are gentle on your hair and kind to the environment.
                  </p>
                  <div class="mt-6 border-t border-slate-200 pt-6">
                    <h3 class="mb-3 font-serif text-xl font-bold text-slate-800">Our Promise</h3>
                    <ul class="grid grid-cols-2 gap-2 text-sm">
                      <li class="flex items-center">
                        <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4 mr-2 text-red-400" viewBox="0 0 20 20" fill="currentColor">
                          <path fill-rule="evenodd" d="M16.707 5.293a1 1 0 010 1.414l-8 8a1 1 0 01-1.414 0l-4-4a1 1 0 011.414-1.414L8 12.586l7.293-7.293a1 1 0 011.414 0z" clip-rule="evenodd" />
                        </svg>
                        Personalized service
                      </li>
                      <li class="flex items-center">
                        <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4 mr-2 text-red-400" viewBox="0 0 20 20" fill="currentColor">
                          <path fill-rule="evenodd" d="M16.707 5.293a1 1 0 010 1.414l-8 8a1 1 0 01-1.414 0l-4-4a1 1 0 011.414-1.414L8 12.586l7.293-7.293a1 1 0 011.414 0z" clip-rule="evenodd" />
                        </svg>
                        Premium products
                      </li>
                      <li class="flex items-center">
                        <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4 mr-2 text-red-400" viewBox="0 0 20 20" fill="currentColor">
                          <path fill-rule="evenodd" d="M16.707 5.293a1 1 0 010 1.414l-8 8a1 1 0 01-1.414 0l-4-4a1 1 0 011.414-1.414L8 12.586l7.293-7.293a1 1 0 011.414 0z" clip-rule="evenodd" />
                        </svg>
                        Expert stylists
                      </li>
                      <li class="flex items-center">
                        <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4 mr-2 text-red-400" viewBox="0 0 20 20" fill="currentColor">
                          <path fill-rule="evenodd" d="M16.707 5.293a1 1 0 010 1.414l-8 8a1 1 0 01-1.414 0l-4-4a1 1 0 011.414-1.414L8 12.586l7.293-7.293a1 1 0 011.414 0z" clip-rule="evenodd" />
                        </svg>
                        Relaxing environment
                      </li>
                    </ul>
                  </div>
                </div>
              </div>
            </div>
          </div>
        {/if}
      </div>
    </section>
    
    <!-- Team Section - Single Member -->
    <section class="py-12 md:py-16">
      <div class="container mx-auto px-6 md:px-12">
        {#if visible}
          <div in:fade={{ duration: 800, delay: 100 }} class="mb-6 text-center">
            <h2 class="font-serif text-3xl font-bold text-slate-800 md:text-4xl">Meet Our Founder</h2>
          </div>
          
          <div class="mx-auto max-w-3xl">
            <!-- Team Member -->
            <div in:fly={{ y: 20, duration: 800, delay: 200 }} class="group overflow-hidden rounded-md bg-white shadow-md transition-transform duration-300 hover:-translate-y-2 flex flex-col md:flex-row">
              <div class="relative w-full md:w-2/5 overflow-hidden">
                <div class="absolute inset-0 bg-red-400 bg-opacity-60 opacity-0 transition-opacity duration-300 group-hover:opacity-60"></div>
                <!-- Replace with actual team member image -->
                <img 
                  src={person}
                  alt="Emma Johnson" 
                  class="h-full w-full object-cover transition-transform duration-500 group-hover:scale-110"
                />
              </div>
              <div class="p-6 w-full md:w-3/5">
                <h3 class="text-xl font-bold text-slate-800">Emma Johnson</h3>
                <p class="text-red-400">Founder & Creative Director</p>
                <p class="mt-3 text-slate-600">With over 15 years of experience in the beauty industry, Emma has built BeautySalon from the ground up with a vision to create a space where clients feel valued and leave looking their absolute best.</p>
                <p class="mt-2 text-slate-600">Her expertise in cutting-edge techniques, combined with her passion for helping clients discover their personal style, has made her one of the most sought-after stylists in the area.</p>
              </div>
            </div>
          </div>
        {/if}
      </div>
    </section>
  </main>
  
  <Footer />