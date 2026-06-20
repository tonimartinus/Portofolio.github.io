<script setup>
import { ref, onMounted, nextTick } from 'vue'

const currentCommand = ref('')
const lines = ref([])
const userInput = ref('')
const isInteractive = ref(false)
const terminalBody = ref(null)

const commandHistory = [
  { input: 'whoami', output: 'Toni Martinus | Freelance Full-Stack Programmer & Automation Engineer.' },
  { input: 'cat core_focus.txt', output: 'Membantu pemilik bisnis dan startup membangun aplikasi web super cepat & otomatisasi data.' },
  { input: 'locate location', output: 'Jakarta, Indonesia (Available for remote projects worldwide).' },
  { input: 'bash init_portfolio.sh', output: 'Loading interactive layout... Done! [Terminal kini INTERAKTIF. Ketik "help" di bawah!]' }
]

const sleep = (ms) => new Promise(resolve => setTimeout(resolve, ms))

const scrollToBottom = () => {
  nextTick(() => {
    if (terminalBody.value) {
      terminalBody.value.scrollTop = terminalBody.value.scrollHeight
    }
  })
}

const runDemoTerminal = async () => {
  await sleep(1000)
  for (const item of commandHistory) {
    currentCommand.value = ''
    for (let i = 0; i < item.input.length; i++) {
      currentCommand.value += item.input[i]
      await sleep(70)
    }
    await sleep(300)
    
    lines.value.push({ type: 'input', text: `$ ${item.input}` })
    currentCommand.value = ''
    
    lines.value.push({ type: 'output', text: item.output })
    scrollToBottom()
    await sleep(600)
  }
  isInteractive.value = true
}

const executeCommand = () => {
  const cmd = userInput.value.trim().toLowerCase()
  if (!cmd) return
  
  lines.value.push({ type: 'input', text: `$ ${userInput.value}` })
  
  if (cmd === 'clear') {
    lines.value = []
  } else if (cmd === 'help') {
    lines.value.push({ type: 'output', text: 'Perintah tersedia: help | whoami | skills | projects | contact | clear' })
  } else if (cmd === 'whoami') {
    lines.value.push({ type: 'output', text: 'Toni Martinus - Seorang full-stack freelance programmer yang fokus pada solusi web (Vue/Tailwind) dan script otomatisasi Python/Node.js.' })
  } else if (cmd === 'skills') {
    lines.value.push({ type: 'output', text: 'Bahasa/Framework: Vue.js 3, Nuxt, Tailwind CSS v4, Node.js, Express, Python Scraper, Postgres, MongoDB, Docker.' })
  } else if (cmd === 'projects') {
    lines.value.push({ type: 'output', text: 'Proyek: RetroPOS.exe (Aplikasi Kasir Web) | ZapScraper.sh (Automation Scraper) | SyncFlow.api (ERP Middleware).' })
  } else if (cmd === 'contact') {
    lines.value.push({ type: 'output', text: 'Email: tonimartinuss@gmail.com | WA: +62 822-1111-0031 | GitHub: github.com/tonimartinus' })
  } else {
    lines.value.push({ type: 'output', text: `bash: command not found: ${cmd}. Ketik "help" untuk melihat bantuan.` })
  }
  
  userInput.value = ''
  scrollToBottom()
}

onMounted(() => {
  runDemoTerminal()
})
</script>

<template>
  <section class="max-w-6xl mx-auto px-4 py-12 md:py-20 grid grid-cols-1 lg:grid-cols-12 gap-8 items-center font-mono">
    <!-- Left Column: Bio / Pitch -->
    <div class="lg:col-span-7 flex flex-col items-start text-black dark:text-white">
      <div class="border-2 border-black bg-retro-amber px-2 py-1 text-black font-bold uppercase text-xs mb-4 neo-shadow animate-pulse">
        🚀 Available for New Projects
      </div>
      
      <h1 class="text-4xl md:text-6xl font-bold font-retro leading-tight tracking-wide mb-6">
        HELLO WORLD, SAYA <span class="bg-retro-green text-black px-2 border-2 border-black">TONI</span>
      </h1>
      
      <p class="text-lg md:text-xl font-sans mb-8 leading-relaxed max-w-xl text-zinc-700 dark:text-zinc-300">
        Saya membuat sistem web modern yang cepat dan efisien dengan desain retro/neo-brutalis. Spesialisasi saya ada di <strong class="underline decoration-retro-green decoration-4">Vue.js</strong>, <strong class="underline decoration-retro-amber decoration-4">Tailwind CSS</strong>, dan <strong class="underline decoration-blue-500 decoration-4">Otomatisasi Script</strong>.
      </p>
      
      <div class="flex flex-wrap gap-4 w-full sm:w-auto">
        <a 
          href="#projects" 
          class="flex-1 sm:flex-none px-6 py-3 bg-retro-green text-black font-bold border-4 border-black neo-shadow neo-shadow-hover neo-shadow-active text-center uppercase tracking-wider transition-all"
        >
          📁 Lihat Portofolio
        </a>
        <a 
          href="#contact" 
          class="flex-1 sm:flex-none px-6 py-3 bg-white dark:bg-zinc-800 text-black dark:text-white font-bold border-4 border-black neo-shadow neo-shadow-hover neo-shadow-active text-center uppercase tracking-wider transition-all"
        >
          ✉️ Hubungi Saya
        </a>
      </div>
    </div>

    <!-- Right Column: Terminal Window Mockup -->
    <div class="lg:col-span-5 w-full">
      <div class="w-full bg-[#1b1c24] text-retro-green neo-border neo-shadow">
        <!-- Terminal Header -->
        <div class="flex items-center justify-between bg-black text-white p-2 border-b-4 border-black font-bold text-xs uppercase">
          <div class="flex items-center gap-2">
            <span class="w-2.5 h-2.5 rounded-full bg-red-600"></span>
            <span class="w-2.5 h-2.5 rounded-full bg-yellow-500"></span>
            <span class="w-2.5 h-2.5 rounded-full bg-green-500"></span>
            <span class="ml-2 font-mono">toni@retro-terminal:~</span>
          </div>
          <span>v1.0.0</span>
        </div>
        
        <!-- Terminal Logs -->
        <div 
          ref="terminalBody"
          class="p-4 h-80 overflow-y-auto font-mono text-sm leading-relaxed flex flex-col gap-2 scrollbar-thin scrollbar-thumb-zinc-700 scrollbar-track-transparent"
        >
          <div class="text-zinc-500">System initialization... OK</div>
          <div class="text-zinc-500">Last login: {{ new Date().toDateString() }}</div>
          
          <div v-for="(line, idx) in lines" :key="idx">
            <span v-if="line.type === 'input'" class="text-white font-bold">{{ line.text }}</span>
            <span v-else class="text-zinc-300 block ml-4">{{ line.text }}</span>
          </div>
          
          <!-- Terminal Command Line: Auto-typing prompt or interactive user input -->
          <div class="flex items-center">
            <span class="text-white font-bold">$ </span>
            
            <template v-if="!isInteractive">
              <span class="text-retro-green ml-1">{{ currentCommand }}</span>
              <span class="animate-pulse bg-retro-green text-transparent ml-1 w-2.5 h-4 inline-block">|</span>
            </template>
            
            <template v-else>
              <input 
                v-model="userInput"
                @keydown.enter="executeCommand"
                type="text"
                placeholder="ketik perintah di sini..."
                class="flex-1 bg-transparent text-retro-green ml-1 border-none outline-none focus:ring-0 p-0 font-mono text-sm placeholder-zinc-700 placeholder-opacity-50"
                autofocus
              />
            </template>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>
