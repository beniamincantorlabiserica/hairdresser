<!-- Footer.svelte -->
<script>
    import { fade, fly } from 'svelte/transition';
    import { onMount } from 'svelte';
    
    // Import your logo if you have one
    // import logo from "$lib/images/logo.webp";
    
    let visible = false;
    
    // Social media links
    const socialLinks = [
      { name: 'Instagram', url: '#', icon: 'instagram' },
      { name: 'Facebook', url: '#', icon: 'facebook' },
    ];
    
    
    onMount(() => {
      // Create an intersection observer to trigger animations when footer is in view
      const observer = new IntersectionObserver((entries) => {
        if (entries[0].isIntersecting) {
          visible = true;
          observer.disconnect();
        }
      }, { threshold: 0.2 });
      
      const footer = document.getElementById('site-footer');
      if (footer) observer.observe(footer);
      
      return () => {
        if (footer) observer.unobserve(footer);
      };
    });
  </script>
  
  <footer id="site-footer" class="relative overflow-hidden bg-slate-900 text-white">
    <!-- Decorative hair scissors in background -->
    <div class="absolute -right-20 top-0 z-0 h-60 w-60 opacity-5">
      <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="currentColor">
        <path d="M9.79289 7.05025C9.42105 6.67841 9.41419 6.06312 9.79289 5.68441L10.5684 4.91892C11.3413 4.146 12.6587 4.146 13.4316 4.91892L14.2071 5.6944C14.5858 6.07311 14.579 6.67841 14.2071 7.05025L13.3229 7.93446C14.7515 9.92991 16.0702 11.9559 17.2782 14.0124C17.6535 14.6124 17.4191 15.3995 16.8191 15.7748C16.2191 16.1501 15.432 15.9157 15.0567 15.3157C13.9395 13.4011 12.7288 11.5102 11.4246 9.64358C10.9286 10.1396 10.4326 10.6356 9.93655 11.1317C8.77402 12.2942 7.6115 13.4567 6.44898 14.6192C5.94452 15.1237 5.66497 15.7864 5.60133 16.5073C5.53768 17.2282 5.73075 17.9491 6.14547 18.5117C6.56019 19.0744 7.16292 19.4539 7.83391 19.6176C8.5049 19.7812 9.27584 19.6881 9.90841 19.3034C10.5085 18.9282 11.2956 19.1626 11.6709 19.7626C12.0462 20.3626 11.8118 21.1497 11.2118 21.525C10.1467 22.1096 8.85743 22.296 7.68741 22.0851C6.38248 21.8478 5.17755 21.1892 4.34842 20.1638C3.51929 19.1384 3.13215 17.8466 3.25879 16.5647C3.38543 15.2829 4.02004 14.0979 4.99999 13.2662C6.2025 12.0637 7.40501 10.8612 8.60752 9.65865C9.00255 9.26362 9.39757 8.8686 9.79289 8.47328V7.05025ZM12.0001 8.20414C12.3536 8.65689 12.7071 9.10963 13.0607 9.56237C14.1779 10.9491 15.2952 12.3358 16.4124 13.7224C16.6415 14.0063 17.0338 14.0568 17.3177 13.8278C17.6017 13.5987 17.6522 13.2064 17.4232 12.9224C16.3059 11.5358 15.1887 10.1491 14.0714 8.76237C13.718 8.31027 13.3645 7.85817 13.0111 7.40607L12.0001 8.20414ZM11.7932 5.68441C11.5 5.39126 11.0235 5.39126 10.7304 5.68441L10.5661 5.84865L11.5661 6.84865L11.7304 6.68441C12.0235 6.39126 12.0235 5.91471 11.7304 5.62157L11.7932 5.68441Z" />
      </svg>
    </div>
    
    <!-- Top section with booking CTA (replacing newsletter) -->
    <div class="border-b border-slate-700/50">
      <div class="container mx-auto px-6 py-12 md:px-12">
        {#if visible}
          <div in:fade={{ duration: 800 }} class="grid grid-cols-1 gap-10 md:grid-cols-2">
            <!-- Left side - salon info -->
            <div>
              <div class="mb-6">
                <!-- You can use your logo here -->
                <h1 class="font-serif text-3xl font-bold text-white">BEAUTY<span class="text-red-400">SALON</span></h1>
              </div>
              
              <p class="mb-6 max-w-md text-slate-300">
                Experience the ultimate in hair care and styling. Our team of professional stylists 
                is dedicated to helping you look and feel your best, with personalized services 
                tailored to your unique style and needs.
              </p>
              
              <div class="flex space-x-4">
                {#each socialLinks as link}
                  <a 
                    href={link.url}
                    aria-label={link.name}
                    class="flex h-10 w-10 items-center justify-center rounded-full border border-slate-700 bg-slate-800 text-slate-300 transition hover:border-red-400 hover:bg-red-400 hover:text-white"
                  >
                    {#if link.icon === 'instagram'}
                      <svg class="h-5 w-5" fill="currentColor" viewBox="0 0 24 24" aria-hidden="true">
                        <path fill-rule="evenodd" d="M12.315 2c2.43 0 2.784.013 3.808.06 1.064.049 1.791.218 2.427.465a4.902 4.902 0 011.772 1.153 4.902 4.902 0 011.153 1.772c.247.636.416 1.363.465 2.427.048 1.067.06 1.407.06 4.123v.08c0 2.643-.012 2.987-.06 4.043-.049 1.064-.218 1.791-.465 2.427a4.902 4.902 0 01-1.153 1.772 4.902 4.902 0 01-1.772 1.153c-.636.247-1.363.416-2.427.465-1.067.048-1.407.06-4.123.06h-.08c-2.643 0-2.987-.012-4.043-.06-1.064-.049-1.791-.218-2.427-.465a4.902 4.902 0 01-1.772-1.153 4.902 4.902 0 01-1.153-1.772c-.247-.636-.416-1.363-.465-2.427-.047-1.024-.06-1.379-.06-3.808v-.63c0-2.43.013-2.784.06-3.808.049-1.064.218-1.791.465-2.427a4.902 4.902 0 011.153-1.772A4.902 4.902 0 015.45 2.525c.636-.247 1.363-.416 2.427-.465C8.901 2.013 9.256 2 11.685 2h.63zm-.081 1.802h-.468c-2.456 0-2.784.011-3.807.058-.975.045-1.504.207-1.857.344-.467.182-.8.398-1.15.748-.35.35-.566.683-.748 1.15-.137.353-.3.882-.344 1.857-.047 1.023-.058 1.351-.058 3.807v.468c0 2.456.011 2.784.058 3.807.045.975.207 1.504.344 1.857.182.466.399.8.748 1.15.35.35.683.566 1.15.748.353.137.882.3 1.857.344 1.054.048 1.37.058 4.041.058h.08c2.597 0 2.917-.01 3.96-.058.976-.045 1.505-.207 1.858-.344.466-.182.8-.398 1.15-.748.35-.35.566-.683.748-1.15.137-.353.3-.882.344-1.857.048-1.055.058-1.37.058-4.041v-.08c0-2.597-.01-2.917-.058-3.96-.045-.976-.207-1.505-.344-1.858a3.097 3.097 0 00-.748-1.15 3.098 3.098 0 00-1.15-.748c-.353-.137-.882-.3-1.857-.344-1.023-.047-1.351-.058-3.807-.058zM12 6.865a5.135 5.135 0 110 10.27 5.135 5.135 0 010-10.27zm0 1.802a3.333 3.333 0 100 6.666 3.333 3.333 0 000-6.666zm5.338-3.205a1.2 1.2 0 110 2.4 1.2 1.2 0 010-2.4z" clip-rule="evenodd" />
                      </svg>
                    {/if}
                    {#if link.icon === 'facebook'}
                      <svg class="h-5 w-5" fill="currentColor" viewBox="0 0 24 24" aria-hidden="true">
                        <path fill-rule="evenodd" d="M22 12c0-5.523-4.477-10-10-10S2 6.477 2 12c0 4.991 3.657 9.128 8.438 9.878v-6.987h-2.54V12h2.54V9.797c0-2.506 1.492-3.89 3.777-3.89 1.094 0 2.238.195 2.238.195v2.46h-1.26c-1.243 0-1.63.771-1.63 1.562V12h2.773l-.443 2.89h-2.33v6.988C18.343 21.128 22 16.991 22 12z" clip-rule="evenodd" />
                      </svg>
                    {/if}
                  </a>
                {/each}
              </div>
            </div>
            
            <!-- Right side - Booking CTA (replacing newsletter) -->
            <div in:fly={{ x: 20, duration: 800, delay: 300 }} class="flex flex-col items-start justify-center rounded-lg bg-slate-800 p-8 shadow-lg">
              <div class="mb-2">
                <span class="inline-block rounded-full bg-red-400 bg-opacity-20 px-3 py-1 text-xs font-medium uppercase tracking-wider text-red-400">Ready for a new look?</span>
              </div>
              
              <h2 class="mb-4 text-2xl font-bold text-white">Book Your Appointment Today</h2>
              
              <p class="mb-6 text-slate-300">
                Don't wait to look your best. Our expert stylists are ready to transform your look with our premium services.
              </p>
              
              <div class="flex w-full flex-col space-y-3 sm:flex-row sm:space-x-4 sm:space-y-0">
                <a 
                  href="/booking" 
                  class="flex-1 rounded-md bg-red-400 px-6 py-3 text-center font-medium text-white transition hover:bg-red-500"
                >
                  Book Online
                </a>
                
                <a 
                  href="tel:+15551234567" 
                  class="flex flex-1 items-center justify-center rounded-md border border-slate-600 px-6 py-3 text-center font-medium text-slate-300 transition hover:border-red-400 hover:text-red-400"
                >
                  <svg xmlns="http://www.w3.org/2000/svg" class="mr-2 h-5 w-5" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 5a2 2 0 012-2h3.28a1 1 0 01.948.684l1.498 4.493a1 1 0 01-.502 1.21l-2.257 1.13a11.042 11.042 0 005.516 5.516l1.13-2.257a1 1 0 011.21-.502l4.493 1.498a1 1 0 01.684.949V19a2 2 0 01-2 2h-1C9.716 21.002 3 14.286 3 8.001V5z" />
                  </svg>
                  Call Us
                </a>
              </div>
            </div>
          </div>
        {/if}
      </div>
    </div>
    
    
    
    <!-- Bottom copyright section -->
    <div class="container mx-auto px-6 py-6 md:px-12">
      {#if visible}
        <div in:fade={{ duration: 800, delay: 600 }} class="flex flex-col items-center justify-between space-y-4 text-center sm:flex-row sm:space-y-0 sm:text-left">
          <p class="text-sm text-slate-400">
            &copy; {new Date().getFullYear()} BeautySalon. All rights reserved.
          </p>
          
          <div class="flex space-x-6 text-sm text-slate-400">
            <a href="/privacy-policy" class="hover:text-red-400">Privacy Policy</a>
            <a href="/terms-of-service" class="hover:text-red-400">Terms of Service</a>
            <a href="/cookie-policy" class="hover:text-red-400">Cookie Policy</a>
          </div>
        </div>
      {/if}
    </div>
  </footer>