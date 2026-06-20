<script setup>
import { ref } from 'vue'

const skills = ref([
  { name: 'Vue.js / Nuxt', level: 90, icon: '🟢' },
  { name: 'Tailwind CSS', level: 95, icon: '🎨' },
  { name: 'Node.js / Express', level: 85, icon: '⚡' },
  { name: 'Python Automations', level: 80, icon: '🐍' },
  { name: 'PostgreSQL / MongoDB', level: 75, icon: '🗄️' },
  { name: 'Git / Docker / Deployment', level: 80, icon: '🚢' }
])

const statistics = ref([
  { label: 'TAHUN PENGALAMAN', value: '3+' },
  { label: 'PROYEK BERHASIL', value: '25+' },
  { label: 'KOPI DIKONSUMSI', value: '412L' },
  { label: 'BUGS DIBASMI', value: '999+' }
])

const avatarUrl = ref('/profile.jpg')
const hasAvatar = ref(true)
const handleAvatarError = () => {
  hasAvatar.value = false
}
</script>

<template>
  <section id="about" class="max-w-6xl mx-auto px-4 py-16 border-t-4 border-black font-mono">
    <!-- Section Title -->
    <div class="inline-block border-4 border-black bg-yellow-300 text-black px-4 py-2 font-retro text-2xl uppercase font-bold neo-shadow mb-12">
      💾 ABOUT_ME.TXT
    </div>

    <div class="grid grid-cols-1 lg:grid-cols-12 gap-12 items-start">
      <!-- Profile Box -->
      <div class="lg:col-span-5 bg-white dark:bg-zinc-900 p-6 neo-border neo-shadow text-black dark:text-white flex flex-col items-center text-center">
        <!-- Avatar Box -->
        <div class="w-48 h-48 border-4 border-black neo-shadow mb-6 overflow-hidden relative bg-retro-green flex items-center justify-center select-none animate-bounce duration-1000">
          <img 
            v-if="hasAvatar"
            :src="avatarUrl" 
            @error="handleAvatarError"
            alt="Toni Martinus" 
            class="w-full h-full object-cover"
          />
          <span v-else class="text-7xl">👨‍💻</span>
        </div>
        <h3 class="text-2xl font-bold uppercase mb-2">Toni Martinus</h3>
        <p class="text-sm font-bold text-zinc-500 uppercase tracking-widest mb-4">&lt; Full-Stack Freelancer /&gt;</p>
        <p class="text-sans text-sm text-zinc-700 dark:text-zinc-300 leading-relaxed mb-6">
          "Saya percaya kode harus bersih, performa harus kencang, dan antarmuka harus memukau. Berfokus pada pemecahan masalah bisnis nyata melalui solusi digital."
        </p>

        <!-- Dynamic Experience Stats -->
        <div class="grid grid-cols-2 gap-4 w-full border-t-2 border-black pt-6">
          <div v-for="(stat, idx) in statistics" :key="idx" class="p-2 border-2 border-black bg-slate-100 dark:bg-zinc-800 neo-shadow">
            <div class="text-2xl font-retro font-bold text-retro-amber">{{ stat.value }}</div>
            <div class="text-[10px] font-bold text-zinc-500 uppercase mt-1 leading-tight">{{ stat.label }}</div>
          </div>
        </div>
      </div>

      <!-- Skills Details -->
      <div id="skills" class="lg:col-span-7 bg-white dark:bg-zinc-900 p-6 neo-border neo-shadow text-black dark:text-white">
        <h3 class="text-xl font-bold uppercase mb-6 flex items-center gap-2">
          <span>📊</span>
          <span>SYSTEM_STATISTICS.EXE (Keahlian)</span>
        </h3>
        <p class="text-sans text-zinc-700 dark:text-zinc-300 mb-8 leading-relaxed">
          Berikut adalah perkiraan tingkat pemahaman dan implementasi praktis teknologi yang sering saya gunakan dalam melayani klien:
        </p>

        <!-- Interactive Skills Progress Bar -->
        <div class="flex flex-col gap-6">
          <div v-for="(skill, idx) in skills" :key="idx" class="w-full">
            <div class="flex justify-between items-center font-bold text-sm mb-2">
              <span class="flex items-center gap-2">
                <span>{{ skill.icon }}</span>
                <span>{{ skill.name }}</span>
              </span>
              <span class="text-retro-amber">{{ skill.level }}%</span>
            </div>
            <!-- Custom Retro Progress bar -->
            <div class="w-full bg-slate-200 dark:bg-zinc-800 border-4 border-black h-8 p-0.5 flex items-center relative overflow-hidden">
              <div 
                class="bg-retro-green h-full border-r-4 border-black transition-all duration-1000"
                :style="{ width: `${skill.level}%` }"
              ></div>
              <!-- Grid background on progress bar -->
              <div class="absolute inset-0 bg-[linear-gradient(90deg,rgba(0,0,0,0.1)_1px,transparent_1px)] bg-[size:16px_100%] pointer-events-none"></div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>
