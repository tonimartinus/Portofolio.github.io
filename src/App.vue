<script setup>
import Navbar from './components/Navbar.vue'
import Hero from './components/Hero.vue'
import About from './components/About.vue'
import Projects from './components/Projects.vue'
import Services from './components/Services.vue'
import Contact from './components/Contact.vue'
</script>

<template>
  <div class="flex flex-col min-h-screen">
    <!-- Navigation Bar -->
    <Navbar />

    <!-- Main Content Section -->
    <main class="flex-grow">
      <!-- Hero Section -->
      <Hero />
      
      <!-- About Me & Skills Section -->
      <About />
      
      <!-- Projects Showcase Section -->
      <Projects />
      
      <!-- Services & Testimonials Section -->
      <Services />
      
      <!-- Contact Form & Socials Section -->
      <Contact />
    </main>

    <!-- Footer -->
    <footer class="w-full bg-white dark:bg-black text-black dark:text-white border-t-4 border-black font-mono py-8 mt-12 text-center text-xs">
      <div class="max-w-6xl mx-auto px-4 space-y-2">
        <p class="font-bold">© {{ new Date().getFullYear() }} TONI.SYS. ALL RIGHTS RESERVED.</p>
        <p class="text-zinc-500">BUILT WITH VUE 3 + TAILWIND CSS v4. RUNNING ON DEBIAN SYSTEM.</p>
      </div>
    </footer>
  </div>
</template>
