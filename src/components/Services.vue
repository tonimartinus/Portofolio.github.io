<script setup>
import { ref } from 'vue'

const services = ref([
  {
    icon: '💻',
    title: 'Aplikasi Web Vue 3',
    desc: 'Pembuatan landing page premium, dashboard admin, atau aplikasi SaaS kustom menggunakan Vue 3, Tailwind CSS, dan integrasi backend yang handal.',
    price: 'Mulai dari Rp5.000.000',
    delivery: 'Estimasi waktu: 7-14 hari kerja'
  },
  {
    icon: '⚙️',
    title: 'Otomatisasi & Scraper',
    desc: 'Automasi entri data manual, web scraping e-commerce secara massal, integrasi bot Telegram/WhatsApp, dan optimasi alur kerja digital Anda.',
    price: 'Mulai dari Rp3.000.000',
    delivery: 'Estimasi waktu: 3-7 hari kerja'
  },
  {
    icon: '🔌',
    title: 'Integrasi API Kustom',
    desc: 'Menghubungkan layanan pihak ketiga (Payment Gateway, Shopify, ERP lokal, Firebase, Maps) ke dalam aplikasi atau infrastruktur server yang sudah ada.',
    price: 'Mulai dari Rp2.500.000',
    delivery: 'Estimasi waktu: 3-5 hari kerja'
  }
])

const testimonials = ref([
  {
    name: 'Budi Santoso',
    role: 'CEO, KopiKuy Retail',
    text: 'Aplikasi RetroPOS buatan Alex mengubah cara kami mengelola transaksi harian. Performanya super kencang di komputer lama kami dan tampilannya disukai pelanggan!',
    avatar: '👨‍💼'
  },
  {
    name: 'Sarah Amalia',
    role: 'Founder, ZapFashion',
    text: 'Skrip scraper dari Alex sangat stabil. Membantu kami mengumpulkan data tren produk e-commerce pesaing secara real-time dan menghemat ratusan jam kerja staf kami.',
    avatar: '👩‍💼'
  }
])
</script>

<template>
  <section id="services" class="max-w-6xl mx-auto px-4 py-16 border-t-4 border-black font-mono">
    <!-- Section Title -->
    <div class="inline-block border-4 border-black bg-retro-amber text-black px-4 py-2 font-retro text-2xl uppercase font-bold neo-shadow mb-12">
      ⚡ AVAILABLE_SERVICES.EXE
    </div>

    <!-- Services Grid -->
    <div class="grid grid-cols-1 md:grid-cols-3 gap-8 mb-16">
      <div 
        v-for="service in services" 
        :key="service.title"
        class="bg-white dark:bg-zinc-900 border-4 border-black p-6 neo-shadow neo-shadow-hover transition-transform duration-100 flex flex-col justify-between"
      >
        <div>
          <!-- Icon & Title -->
          <div class="text-4xl mb-4 border-2 border-black bg-slate-100 dark:bg-zinc-800 w-12 h-12 flex items-center justify-center neo-shadow">
            {{ service.icon }}
          </div>
          <h3 class="text-xl font-bold uppercase mb-3 text-black dark:text-white">
            {{ service.title }}
          </h3>
          <p class="text-sans text-sm text-zinc-600 dark:text-zinc-400 leading-relaxed mb-6">
            {{ service.desc }}
          </p>
        </div>

        <!-- Pricing & Timeline details -->
        <div class="border-t-2 border-black pt-4 mt-4 text-xs font-bold space-y-1.5 text-zinc-700 dark:text-zinc-300">
          <div class="flex justify-between items-center">
            <span>HARGA:</span>
            <span class="text-retro-amber font-retro text-base font-bold">{{ service.price }}</span>
          </div>
          <div class="flex justify-between items-center text-zinc-500">
            <span>DURASI:</span>
            <span>{{ service.delivery }}</span>
          </div>
        </div>
      </div>
    </div>

    <!-- Testimonials Divider -->
    <div class="mt-16 pt-16 border-t-4 border-dashed border-black dark:border-zinc-800">
      <div class="inline-block border-2 border-black bg-zinc-200 dark:bg-zinc-800 text-black dark:text-white px-3 py-1 font-bold text-xs uppercase mb-8">
        ⭐ BUKTI_SOSIAL.TXT (Ulasan Klien)
      </div>

      <div class="grid grid-cols-1 md:grid-cols-2 gap-8">
        <div 
          v-for="testi in testimonials" 
          :key="testi.name"
          class="bg-white dark:bg-zinc-900 border-4 border-black p-6 neo-shadow relative flex flex-col justify-between"
        >
          <!-- Retro Chat bubble indicator -->
          <div class="absolute -top-4 left-6 text-2xl font-bold text-retro-green">
            💬
          </div>
          
          <p class="text-sans text-sm text-zinc-700 dark:text-zinc-300 italic leading-relaxed mb-6">
            "{{ testi.text }}"
          </p>
          
          <!-- Client Avatar & Profile info -->
          <div class="flex items-center gap-3">
            <span class="w-10 h-10 border-2 border-black bg-retro-green flex items-center justify-center text-xl neo-shadow">
              {{ testi.avatar }}
            </span>
            <div>
              <h4 class="font-bold text-sm text-black dark:text-white">{{ testi.name }}</h4>
              <p class="text-[10px] font-bold text-zinc-500 uppercase">{{ testi.role }}</p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>
