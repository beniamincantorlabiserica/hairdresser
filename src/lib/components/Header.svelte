<script>
  import { onMount } from 'svelte';
  import { fade, fly, scale } from 'svelte/transition';
  import { cubicOut } from 'svelte/easing';
  import { page } from '$app/stores';
  
  let isMenuOpen = false;
  let scrollY;
  let isScrolled = false;
  
  // Navigation items with path and label
  const navItems = [
    { path: '/', label: 'Home' },
    { path: '/about', label: 'About' },
    { path: '/gallery', label: 'Gallery' },
  ];
  
  function toggleMenu() {
    isMenuOpen = !isMenuOpen;
    
    // Prevent scrolling when menu is open
    if (isMenuOpen) {
      document.body.style.overflow = 'hidden';
    } else {
      document.body.style.overflow = '';
    }
  }
  
  // Close mobile menu when clicking outside
  function handleClickOutside(event) {
    if (isMenuOpen && !event.target.closest('nav') && !event.target.closest('button.menu-toggle')) {
      isMenuOpen = false;
      document.body.style.overflow = '';
    }
  }
  
  // Helper function to check if a path is active
  function isActive(path) {
    if (path === '/') {
      return $page.url.pathname === path;
    }
    return $page.url.pathname.startsWith(path);
  }
  
  onMount(() => {
    document.addEventListener('click', handleClickOutside);
    return () => {
      document.removeEventListener('click', handleClickOutside);
      document.body.style.overflow = '';
    };
  });
  
  // Handle scroll for shadow effect
  function handleScroll() {
    isScrolled = scrollY > 50;
  }
</script>

<svelte:window bind:scrollY on:scroll={handleScroll} />

<header class={`fixed w-full z-50 transition-all duration-300 bg-white ${isScrolled ? 'shadow-md' : ''}`}>
  <div class="relative">
    <!-- Fading bottom edge -->
    <div class="absolute bottom-0 left-0 right-0 h-4 bg-gradient-to-b from-transparent to-gray-100/20"></div>
    
    <div class="container mx-auto flex justify-between items-center px-6 py-4">
      <!-- Logo Area - Increased space -->
      <a href="/" class="flex items-center z-50 relative">
        <!-- Logo or text can go here -->
        <div class="w-48">
          <span class="italic mr-1 text-xl text-red-400">h</span>
          <span class="text-lg font-medium tracking-wider text-slate-800">HAIRDRESSER</span>
        </div>
      </a>
      
      <!-- Desktop Navigation -->
      <nav class="hidden md:flex items-center space-x-8">
        {#each navItems as item}
          <a 
            href={item.path} 
            class={`text-slate-800 hover:text-red-400 uppercase text-sm font-medium tracking-wider transition-all 
            ${isActive(item.path) ? 'border-b-2 border-red-400' : 'hover:border-b-2 hover:border-red-400'}`}
          >
            {item.label}
          </a>
        {/each}
      </nav>
      
      <!-- CTA Button -->
      <button class="hidden md:inline-block border-2 border-red-400 text-red-400 hover:bg-red-400 hover:text-white px-5 py-2 text-sm uppercase tracking-wider transition duration-300 rounded-full">
        Book Now
      </button>
      
      <!-- Mobile Menu Button -->
      <button 
        class="menu-toggle md:hidden text-slate-800 focus:outline-none z-50 relative" 
        on:click={toggleMenu} 
        aria-label="Toggle menu"
      >
        <div class="relative w-6 h-6">
          <span class={`absolute h-0.5 w-6 bg-slate-800 transform transition-all duration-300 ease-in-out ${isMenuOpen ? 'rotate-45 top-3' : 'top-1'}`}></span>
          <span class={`absolute h-0.5 w-6 bg-slate-800 top-3 transition-all duration-300 ease-in-out ${isMenuOpen ? 'opacity-0' : 'opacity-100'}`}></span>
          <span class={`absolute h-0.5 w-6 bg-slate-800 transform transition-all duration-300 ease-in-out ${isMenuOpen ? '-rotate-45 top-3' : 'top-5'}`}></span>
        </div>
      </button>
    </div>
  </div>
  
  <!-- Fullscreen Mobile Navigation with Animation -->
  {#if isMenuOpen}
    <div 
      class="fixed inset-0 bg-white z-40" 
      transition:fade={{ duration: 300 }}
    >
      <nav class="h-full flex flex-col justify-center items-center px-6 pt-20 pb-10">
        <div class="flex flex-col items-center space-y-6 w-full max-w-md">
          {#each navItems as item, i}
            <a 
              href={item.path} 
              class={`text-slate-800 hover:text-red-400 py-2 uppercase text-lg font-medium tracking-wider w-full text-center
              ${isActive(item.path) ? 'text-red-400' : ''}`}
              on:click={toggleMenu}
              in:fly={{ y: 20, duration: 300, delay: 100 + (i * 50), easing: cubicOut }}
            >
              {item.label}
              <div class="h-px w-full bg-gradient-to-r from-transparent via-gray-200 to-transparent mt-2"></div>
            </a>
          {/each}
          
          <button 
            class="border-2 border-red-400 text-red-400 hover:bg-red-400 hover:text-white px-8 py-3 text-sm uppercase tracking-wider transition duration-300 rounded-full mt-8 w-full max-w-xs"
            on:click={toggleMenu}
            in:scale={{ start: 0.9, duration: 300, delay: 500, easing: cubicOut }}
          >
            Book Now
          </button>
          
          <!-- Social icons -->
          <div 
            class="flex space-x-6 mt-10"
            in:fade={{ duration: 300, delay: 650 }}
          >
            <a href="#" class="text-slate-400 hover:text-red-400 transition-colors">
              <svg class="h-6 w-6" fill="currentColor" viewBox="0 0 24 24" aria-hidden="true">
                <path fill-rule="evenodd" d="M22 12c0-5.523-4.477-10-10-10S2 6.477 2 12c0 4.991 3.657 9.128 8.438 9.878v-6.987h-2.54V12h2.54V9.797c0-2.506 1.492-3.89 3.777-3.89 1.094 0 2.238.195 2.238.195v2.46h-1.26c-1.243 0-1.63.771-1.63 1.562V12h2.773l-.443 2.89h-2.33v6.988C18.343 21.128 22 16.991 22 12z" clip-rule="evenodd" />
              </svg>
            </a>
            <a href="#" class="text-slate-400 hover:text-red-400 transition-colors">
              <svg class="h-6 w-6" fill="currentColor" viewBox="0 0 24 24" aria-hidden="true">
                <path fill-rule="evenodd" d="M12.315 2c2.43 0 2.784.013 3.808.06 1.064.049 1.791.218 2.427.465a4.902 4.902 0 011.772 1.153 4.902 4.902 0 011.153 1.772c.247.636.416 1.363.465 2.427.048 1.067.06 1.407.06 4.123v.08c0 2.643-.012 2.987-.06 4.043-.049 1.064-.218 1.791-.465 2.427a4.902 4.902 0 01-1.153 1.772 4.902 4.902 0 01-1.772 1.153c-.636.247-1.363.416-2.427.465-1.067.048-1.407.06-4.123.06h-.08c-2.643 0-2.987-.012-4.043-.06-1.064-.049-1.791-.218-2.427-.465a4.902 4.902 0 01-1.772-1.153 4.902 4.902 0 01-1.153-1.772c-.247-.636-.416-1.363-.465-2.427-.047-1.024-.06-1.379-.06-3.808v-.63c0-2.43.013-2.784.06-3.808.049-1.064.218-1.791.465-2.427a4.902 4.902 0 011.153-1.772A4.902 4.902 0 015.45 2.525c.636-.247 1.363-.416 2.427-.465C8.901 2.013 9.256 2 11.685 2h.63zm-.081 1.802h-.468c-2.456 0-2.784.011-3.807.058-.975.045-1.504.207-1.857.344-.467.182-.8.398-1.15.748-.35.35-.566.683-.748 1.15-.137.353-.3.882-.344 1.857-.047 1.023-.058 1.351-.058 3.807v.468c0 2.456.011 2.784.058 3.807.045.975.207 1.504.344 1.857.182.466.399.8.748 1.15.35.35.683.566 1.15.748.353.137.882.3 1.857.344 1.054.048 1.37.058 4.041.058h.08c2.597 0 2.917-.01 3.96-.058.976-.045 1.505-.207 1.858-.344.466-.182.8-.398 1.15-.748.35-.35.566-.683.748-1.15.137-.353.3-.882.344-1.857.048-1.055.058-1.37.058-4.041v-.08c0-2.597-.01-2.917-.058-3.96-.045-.976-.207-1.505-.344-1.858a3.097 3.097 0 00-.748-1.15 3.098 3.098 0 00-1.15-.748c-.353-.137-.882-.3-1.857-.344-1.023-.047-1.351-.058-3.807-.058zM12 6.865a5.135 5.135 0 110 10.27 5.135 5.135 0 010-10.27zm0 1.802a3.333 3.333 0 100 6.666 3.333 3.333 0 000-6.666zm5.338-3.205a1.2 1.2 0 110 2.4 1.2 1.2 0 010-2.4z" clip-rule="evenodd" />
              </svg>
            </a>
          </div>
          
          <!-- Contact info -->
          <div 
            class="mt-10 text-center text-slate-500 text-sm"
            in:fade={{ duration: 300, delay: 750 }}
          >
            <p>123 Beauty Street, Suite 100</p>
            <p class="mt-1">+1 (555) 123-4567</p>
          </div>
        </div>
      </nav>
    </div>
  {/if}
</header>