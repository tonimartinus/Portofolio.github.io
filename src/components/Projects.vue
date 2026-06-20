<script setup>
import { ref, computed } from 'vue'
import WindowModal from './WindowModal.vue'

const categories = ['All', 'Web App', 'Automations', 'API Integration']
const activeCategory = ref('All')

const projects = ref([
  {
    id: 1,
    title: 'RetroPOS.exe',
    category: 'Web App',
    shortDesc: 'Aplikasi kasir web-based dengan tampilan retro OS kustom untuk kedai kopi lokal.',
    longDesc: 'RetroPOS adalah sistem Point-of-Sale (POS) berbasis web yang dirancang khusus untuk toko ritel kecil dan kedai kopi. Dikembangkan dengan Vue 3 dan Tailwind CSS untuk memberikan UI bertema retro Windows 95 yang responsif dan sangat ringan. Terintegrasi dengan database lokal dan printer struk termal.',
    tags: ['Vue 3', 'Tailwind CSS', 'IndexedDB', 'Web Serial API'],
    problem: 'Pemilik kedai kopi menginginkan sistem POS yang efisien, tidak membebani browser komputer lama mereka, dan memiliki estetika visual unik yang membedakannya dari POS modern yang seragam.',
    solution: 'Membangun aplikasi POS single-page yang super cepat dengan caching lokal (IndexedDB) sehingga tetap berfungsi penuh meskipun koneksi internet terputus, dibalut desain visual retro klasik.',
    demoUrl: '#',
    githubUrl: '#'
  },
  {
    id: 2,
    title: 'ZapScraper.sh',
    category: 'Automations',
    shortDesc: 'Skrip otomatis pengikis harga produk e-commerce & bot notifikasi telegram.',
    longDesc: 'ZapScraper adalah solusi otomatisasi berbasis Node.js dan Python yang secara berkala memeriksa harga produk dari berbagai situs e-commerce, membandingkannya, dan mengirimkan alert instan ke Telegram ketika ada penurunan harga signifikan.',
    tags: ['Python', 'Node.js', 'Playwright', 'Telegram Bot API', 'Cron Jobs'],
    problem: 'Klien menghabiskan waktu hingga 3 jam sehari secara manual memantau harga kompetitor untuk menyesuaikan harga jual produk mereka.',
    solution: 'Otomatisasi pengikisan data dengan Playwright yang berjalan di latar belakang (VPS) setiap 1 jam, dengan dasbor analitik web sederhana untuk memantau tren harga.',
    demoUrl: '#',
    githubUrl: '#'
  },
  {
    id: 3,
    title: 'SyncFlow.api',
    category: 'API Integration',
    shortDesc: 'Integrasi middleware real-time sinkronisasi stok antara Shopify dan sistem ERP lokal.',
    longDesc: 'SyncFlow adalah API middleware kustom yang bertindak sebagai jembatan sinkronisasi data stok barang secara real-time dari toko online Shopify ke server ERP database PostgreSQL milik pabrik lokal.',
    tags: ['Node.js', 'Express', 'Shopify Webhooks', 'PostgreSQL', 'Redis'],
    problem: 'Sering terjadi pembatalan pesanan karena perbedaan data stok antara gudang fisik (ERP) dan etalase Shopify, yang merugikan reputasi toko.',
    solution: 'Menghubungkan webhook Shopify dengan Redis queue untuk memproses pembaruan stok secara instan di latar belakang tanpa adanya bottleneck data.',
    demoUrl: '#',
    githubUrl: '#'
  },
  {
    id: 4,
    title: 'NeonTasks.bin',
    category: 'Web App',
    shortDesc: 'Aplikasi manajemen tugas bergaya Kanban papan tulis neon untuk tim pengembang.',
    longDesc: 'NeonTasks adalah papan Kanban kolaboratif sederhana yang menonjolkan estetika retro Cyberpunk/Neon. Membantu pengembang memantau progres tugas harian mereka dengan drag-and-drop yang sangat intuitif.',
    tags: ['Vue 3', 'Tailwind CSS', 'Firebase Firestore', 'HTML5 Drag & Drop'],
    problem: 'Tim pengembang bosan dengan Trello atau Jira yang berantakan dan lambat, mencari papan visual yang sederhana dan menyenangkan untuk digunakan.',
    solution: 'Membuat aplikasi papan kanban real-time kolaboratif dengan backend serverless Firebase, dioptimalkan untuk kecepatan pemuatan di bawah 1 detik.',
    demoUrl: '#',
    githubUrl: '#'
  }
])

const filteredProjects = computed(() => {
  if (activeCategory.value === 'All') return projects.value
  return projects.value.filter(p => p.category === activeCategory.value)
})

// Modal state management
const isModalOpen = ref(false)
const selectedProject = ref(null)

const openProjectDetail = (project) => {
  selectedProject.value = project
  isModalOpen.value = true
}

const closeModal = () => {
  isModalOpen.value = false
  selectedProject.value = null
}
</script>

<template>
  <section id="projects" class="max-w-6xl mx-auto px-4 py-16 border-t-4 border-black font-mono">
    <!-- Section Header -->
    <div class="inline-block border-4 border-black bg-retro-green text-black px-4 py-2 font-retro text-2xl uppercase font-bold neo-shadow mb-12">
      📂 CLIENT_PROJECTS.EXE
    </div>

    <!-- Category Filters -->
    <div class="flex flex-wrap gap-2 mb-10">
      <button 
        v-for="cat in categories" 
        :key="cat"
        @click="activeCategory = cat"
        class="px-4 py-2 border-2 border-black font-bold uppercase text-xs sm:text-sm cursor-pointer transition-all duration-100"
        :class="[
          activeCategory === cat 
            ? 'bg-black text-white dark:bg-white dark:text-black translate-y-[1px]' 
            : 'bg-white dark:bg-zinc-800 text-black dark:text-white hover:bg-zinc-200 dark:hover:bg-zinc-700'
        ]"
      >
        * {{ cat }}
      </button>
    </div>

    <!-- Project Grid -->
    <div class="grid grid-cols-1 md:grid-cols-2 gap-8">
      <div 
        v-for="project in filteredProjects" 
        :key="project.id"
        class="bg-white dark:bg-zinc-900 border-4 border-black p-6 neo-shadow neo-shadow-hover transition-transform duration-100 flex flex-col justify-between"
      >
        <div>
          <!-- Title & Category Badge -->
          <div class="flex justify-between items-start mb-4">
            <span class="text-xl font-bold bg-zinc-200 dark:bg-zinc-800 px-2 py-0.5 border-2 border-black text-black dark:text-white">
              {{ project.title }}
            </span>
            <span class="text-xs font-bold uppercase bg-retro-amber border-2 border-black px-2 py-0.5 text-black">
              {{ project.category }}
            </span>
          </div>

          <!-- Short Description -->
          <p class="text-sans text-sm text-zinc-700 dark:text-zinc-300 leading-relaxed mb-6">
            {{ project.shortDesc }}
          </p>

          <!-- Tech Tags -->
          <div class="flex flex-wrap gap-1.5 mb-6">
            <span 
              v-for="tag in project.tags" 
              :key="tag"
              class="text-[10px] font-bold px-2 py-0.5 bg-slate-100 dark:bg-zinc-800 text-zinc-600 dark:text-zinc-400 border border-zinc-300 dark:border-zinc-700"
            >
              #{{ tag }}
            </span>
          </div>
        </div>

        <!-- Call to Action -->
        <button 
          @click="openProjectDetail(project)"
          class="w-full text-center py-2 bg-retro-green hover:bg-emerald-400 text-black font-bold border-2 border-black uppercase text-sm neo-shadow-active hover:translate-y-[1px] cursor-pointer"
        >
          🔍 Buka Detail Proyek
        </button>
      </div>
    </div>

    <!-- Window Modal for Project Detail -->
    <WindowModal 
      v-if="selectedProject"
      :title="selectedProject.title"
      :is-open="isModalOpen"
      @close="closeModal"
    >
      <div class="space-y-6">
        <!-- Badge -->
        <div class="flex items-center justify-between">
          <h2 class="text-2xl font-bold uppercase underline">{{ selectedProject.title }}</h2>
          <span class="px-2 py-1 bg-retro-amber border-2 border-black text-xs font-bold text-black uppercase">
            {{ selectedProject.category }}
          </span>
        </div>

        <!-- Description -->
        <p class="text-sans text-zinc-700 dark:text-zinc-300 leading-relaxed">
          {{ selectedProject.longDesc }}
        </p>

        <!-- Problem / Solution layout -->
        <div class="grid grid-cols-1 md:grid-cols-2 gap-4 pt-4 border-t border-zinc-200 dark:border-zinc-800">
          <div class="p-3 bg-red-50 dark:bg-red-950/20 border-2 border-red-200 dark:border-red-900/50">
            <h4 class="text-red-700 dark:text-red-400 font-bold uppercase text-xs mb-2">⚠️ TANTANGAN KLIEN:</h4>
            <p class="text-sans text-sm text-zinc-700 dark:text-zinc-300 leading-relaxed">{{ selectedProject.problem }}</p>
          </div>
          <div class="p-3 bg-emerald-50 dark:bg-emerald-950/20 border-2 border-emerald-200 dark:border-emerald-900/50">
            <h4 class="text-emerald-700 dark:text-emerald-400 font-bold uppercase text-xs mb-2">✨ SOLUSI SAYA:</h4>
            <p class="text-sans text-sm text-zinc-700 dark:text-zinc-300 leading-relaxed">{{ selectedProject.solution }}</p>
          </div>
        </div>

        <!-- Tech Stack Tags in Modal -->
        <div>
          <h4 class="font-bold text-xs uppercase text-zinc-500 mb-2">TEKNOLOGI YANG DIGUNAKAN:</h4>
          <div class="flex flex-wrap gap-2">
            <span 
              v-for="tag in selectedProject.tags" 
              :key="tag"
              class="text-xs font-bold px-3 py-1 bg-zinc-200 dark:bg-zinc-800 text-black dark:text-white border-2 border-black"
            >
              {{ tag }}
            </span>
          </div>
        </div>

        <!-- Footer Actions in Modal -->
        <div class="flex flex-wrap gap-3 pt-6 border-t-2 border-black justify-end">
          <a 
            :href="selectedProject.githubUrl"
            class="px-4 py-2 border-2 border-black text-black dark:text-white font-bold text-xs uppercase hover:bg-zinc-200 dark:hover:bg-zinc-800 transition-colors"
          >
            💻 Lihat Kode GitHub
          </a>
          <a 
            :href="selectedProject.demoUrl"
            class="px-4 py-2 bg-retro-green border-2 border-black text-black font-bold text-xs uppercase hover:bg-emerald-400 transition-colors"
          >
            ⚡ Live Demo
          </a>
        </div>
      </div>
    </WindowModal>
  </section>
</template>
