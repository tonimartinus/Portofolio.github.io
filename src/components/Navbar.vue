<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

const timeString = ref('')
const cpuUsage = ref(8)
const ramUsage = ref(42)
let timerId = null

const updateClockAndStats = () => {
  const now = new Date()
  const hrs = String(now.getHours()).padStart(2, '0')
  const mins = String(now.getMinutes()).padStart(2, '0')
  const secs = String(now.getSeconds()).padStart(2, '0')
  timeString.value = `${hrs}:${mins}:${secs}`
  
  // Fluktuasi statistik CPU & RAM agar terasa seperti OS aktif
  cpuUsage.value = Math.floor(Math.random() * 18) + 4 // 4% - 22%
  ramUsage.value = Math.floor(Math.random() * 6) + 41 // 41% - 46%
}

const isDark = ref(true)

const toggleTheme = () => {
  isDark.value = !isDark.value
  const html = document.documentElement
  if (isDark.value) {
    html.classList.add('dark')
  } else {
    html.classList.remove('dark')
  }
}

onMounted(() => {
  updateClockAndStats()
  timerId = setInterval(updateClockAndStats, 1000)
  
  // Set default theme state based on DOM
  isDark.value = document.documentElement.classList.contains('dark')
})

onUnmounted(() => {
  if (timerId) clearInterval(timerId)
})
</script>

<template>
  <header class="sticky top-0 z-40 w-full bg-white dark:bg-black text-black dark:text-white border-b-4 border-black font-mono">
    <div class="max-w-6xl mx-auto px-4 py-2 flex items-center justify-between flex-wrap gap-3">
      <!-- Brand Logo -->
      <a href="#" class="flex items-center gap-2 font-bold text-lg border-2 border-black px-2 py-1 bg-retro-green dark:bg-retro-green text-black neo-shadow-hover transition-transform duration-100">
        <span>📟</span>
        <span>TONI.SYS</span>
      </a>

      <!-- Navigation Links -->
      <nav class="flex items-center gap-1 sm:gap-4 flex-wrap text-sm uppercase font-bold">
        <a href="#about" class="hover:bg-black hover:text-white dark:hover:bg-white dark:hover:text-black px-2 py-1 border-2 border-transparent hover:border-black transition-all">
          [About]
        </a>
        <a href="#skills" class="hover:bg-black hover:text-white dark:hover:bg-white dark:hover:text-black px-2 py-1 border-2 border-transparent hover:border-black transition-all">
          [Skills]
        </a>
        <a href="#projects" class="hover:bg-black hover:text-white dark:hover:bg-white dark:hover:text-black px-2 py-1 border-2 border-transparent hover:border-black transition-all">
          [Projects]
        </a>
        <a href="#services" class="hover:bg-black hover:text-white dark:hover:bg-white dark:hover:text-black px-2 py-1 border-2 border-transparent hover:border-black transition-all">
          [Services]
        </a>
        <a href="#contact" class="hover:bg-black hover:text-white dark:hover:bg-white dark:hover:text-black px-2 py-1 border-2 border-transparent hover:border-black transition-all">
          [Contact]
        </a>
      </nav>

      <!-- System Controls & Time -->
      <div class="flex items-center gap-3 text-sm font-bold ml-auto sm:ml-0">
        <!-- Theme Toggle -->
        <button 
          @click="toggleTheme"
          class="px-2 py-1 border-2 border-black bg-yellow-300 dark:bg-zinc-800 text-black dark:text-white hover:translate-y-[1px] cursor-pointer flex items-center gap-1"
          title="Toggle System Theme"
        >
          <span>{{ isDark ? '☀️' : '🌙' }}</span>
          <span class="hidden md:inline">{{ isDark ? 'LIGHT' : 'DARK' }}</span>
        </button>

        <!-- System Resources (CPU/RAM) -->
        <div class="hidden md:flex items-center gap-2 border-2 border-black bg-slate-100 dark:bg-zinc-950 px-2.5 py-1 text-[11px] text-zinc-500 font-bold">
          <span>CPU: <span class="text-retro-amber font-mono">{{ cpuUsage }}%</span></span>
          <span class="text-zinc-300 dark:text-zinc-800">|</span>
          <span>RAM: <span class="text-retro-amber font-mono">{{ ramUsage }}%</span></span>
        </div>

        <!-- System Clock -->
        <div class="border-2 border-black bg-slate-200 dark:bg-zinc-900 px-3 py-1 text-black dark:text-retro-green">
          <span>🕒 {{ timeString || '00:00:00' }}</span>
        </div>
      </div>
    </div>
  </header>
</template>
