<script setup>
import { ref } from 'vue'

const form = ref({
  name: '',
  email: '',
  subject: 'KONSULTASI_PROYEK',
  message: ''
})

const honeypot = ref('') // Field rahasia anti-spam (honeypot)
const isSending = ref(false)
const isSent = ref(false)

// Fungsi sanitasi input sederhana untuk menghilangkan tag HTML (proteksi XSS)
const sanitizeInput = (val) => {
  if (typeof val !== 'string') return ''
  return val.replace(/<[^>]*>/g, '').trim()
}

const handleSubmit = async () => {
  // 1. Cek Honeypot (jika diisi oleh bot otomatis)
  if (honeypot.value) {
    // Diam-diam anggap sukses agar bot tidak tahu bahwa mereka diblokir
    isSent.value = true
    form.value = { name: '', email: '', subject: 'KONSULTASI_PROYEK', message: '' }
    honeypot.value = ''
    return
  }

  // 2. Validasi input wajib
  if (!form.value.name || !form.value.email || !form.value.message) {
    alert('Harap lengkapi semua bidang sebelum mengirim!')
    return
  }

  // 3. Validasi format email secara ketat
  const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/
  if (!emailRegex.test(form.value.email)) {
    alert('Format email balasan tidak valid!')
    return
  }
  
  isSending.value = true

  // 4. Sanitasi input dari tag HTML berbahaya
  const cleanName = sanitizeInput(form.value.name)
  const cleanEmail = sanitizeInput(form.value.email)
  const cleanMessage = sanitizeInput(form.value.message)
  
  try {
    const response = await fetch('https://formsubmit.co/ajax/tonimartinuss@gmail.com', {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json',
        'Accept': 'application/json'
      },
      body: JSON.stringify({
        name: cleanName,
        email: cleanEmail,
        subject: form.value.subject,
        message: cleanMessage,
        _honey: honeypot.value, // Kirim honeypot kosong untuk verifikasi FormSubmit
        _subject: `Pesan Portofolio: ${form.value.subject}`
      })
    })
    
    if (response.ok) {
      isSent.value = true
      form.value = {
        name: '',
        email: '',
        subject: 'KONSULTASI_PROYEK',
        message: ''
      }
    } else {
      alert('Gagal mengirim pesan. Silakan coba lagi.')
    }
  } catch (error) {
    alert('Terjadi kesalahan jaringan. Silakan hubungi langsung melalui WhatsApp.')
  } finally {
    isSending.value = false
  }
}
</script>

<template>
  <section id="contact" class="max-w-6xl mx-auto px-4 py-16 border-t-4 border-black font-mono">
    <!-- Section Title -->
    <div class="inline-block border-4 border-black bg-retro-green text-black px-4 py-2 font-retro text-2xl uppercase font-bold neo-shadow mb-12">
      ✉️ SEND_MESSAGE.EXE
    </div>

    <div class="grid grid-cols-1 lg:grid-cols-12 gap-12 items-start">
      <!-- Contact Form Box (Looks like an email client or retro dialog window) -->
      <div class="lg:col-span-7 bg-white dark:bg-zinc-900 border-4 border-black neo-shadow text-black dark:text-white">
        <!-- Window Title Bar -->
        <div class="flex items-center justify-between bg-black text-white dark:bg-white dark:text-black p-2 font-mono text-xs uppercase font-bold border-b-4 border-black">
          <div class="flex items-center gap-2">
            <span>✉️</span>
            <span>compose_email.exe</span>
          </div>
          <div class="flex items-center gap-1">
            <span class="w-2.5 h-2.5 bg-zinc-600 rounded-full border border-black"></span>
            <span class="w-2.5 h-2.5 bg-zinc-600 rounded-full border border-black"></span>
          </div>
        </div>

        <!-- Form content -->
        <form @submit.prevent="handleSubmit" class="p-6 space-y-4">
          <!-- Honeypot (Anti-Spam) Field: Hidden for normal users, bots will auto-fill it -->
          <div class="hidden" aria-hidden="true">
            <input 
              v-model="honeypot" 
              type="text" 
              name="_honey" 
              tabindex="-1" 
              autocomplete="off" 
            />
          </div>
          <!-- Name Input -->
          <div class="flex flex-col gap-1.5">
            <label class="text-xs font-bold uppercase text-zinc-500">Dari (Nama Anda):</label>
            <input 
              v-model="form.name"
              type="text" 
              placeholder="Contoh: Budi Santoso"
              required
              class="w-full bg-slate-100 dark:bg-zinc-800 text-black dark:text-white border-2 border-black p-2 font-bold focus:outline-none focus:bg-retro-green/10"
            />
          </div>

          <!-- Email Input -->
          <div class="flex flex-col gap-1.5">
            <label class="text-xs font-bold uppercase text-zinc-500">Email Balasan:</label>
            <input 
              v-model="form.email"
              type="email" 
              placeholder="budi@example.com"
              required
              class="w-full bg-slate-100 dark:bg-zinc-800 text-black dark:text-white border-2 border-black p-2 font-bold focus:outline-none focus:bg-retro-green/10"
            />
          </div>

          <!-- Subject Selection -->
          <div class="flex flex-col gap-1.5">
            <label class="text-xs font-bold uppercase text-zinc-500">Subjek:</label>
            <select 
              v-model="form.subject"
              class="w-full bg-slate-100 dark:bg-zinc-800 text-black dark:text-white border-2 border-black p-2 font-bold focus:outline-none focus:bg-retro-green/10"
            >
              <option value="KONSULTASI_PROYEK">KONSULTASI_PROYEK.TXT (Kerja Sama)</option>
              <option value="TANYA_JASA">PERTANYAAN_JASA.INI (Informasi Layanan)</option>
              <option value="SAY_HELLO">SAY_HELLO.EXE (Sapa Saja)</option>
            </select>
          </div>

          <!-- Message Textarea -->
          <div class="flex flex-col gap-1.5">
            <label class="text-xs font-bold uppercase text-zinc-500">Pesan / Detail Proyek:</label>
            <textarea 
              v-model="form.message"
              rows="5"
              placeholder="Tulis ide aplikasi Anda atau apa yang ingin didiskusikan..."
              required
              class="w-full bg-slate-100 dark:bg-zinc-800 text-black dark:text-white border-2 border-black p-2 font-bold focus:outline-none focus:bg-retro-green/10"
            ></textarea>
          </div>

          <!-- Success Alert Bubble -->
          <div 
            v-if="isSent" 
            class="p-3 bg-emerald-50 dark:bg-emerald-950/20 border-2 border-emerald-500 text-emerald-800 dark:text-emerald-400 font-bold text-sm uppercase flex items-center justify-between"
          >
            <span>🟢 Pesan terkirim! Saya akan membalas via email.</span>
            <button @click="isSent = false" type="button" class="underline cursor-pointer hover:text-black">tutup</button>
          </div>

          <!-- Submit Button -->
          <button 
            type="submit"
            :disabled="isSending"
            class="w-full py-3 font-bold uppercase text-sm border-2 border-black text-black bg-retro-green hover:bg-emerald-400 disabled:bg-zinc-500 cursor-pointer neo-shadow-active hover:translate-y-[1px]"
          >
            {{ isSending ? '🔄 SEDANG MENGIRIM...' : '✉️ KIRIM PESAN' }}
          </button>
        </form>
      </div>

      <!-- Quick Connections / Social Links -->
      <div class="lg:col-span-5 space-y-6">
        <div class="bg-white dark:bg-zinc-900 border-4 border-black p-6 neo-shadow text-black dark:text-white">
          <h3 class="text-lg font-bold uppercase mb-4">⚡ DIREKTORI_KONTAK</h3>
          <p class="text-sans text-sm text-zinc-600 dark:text-zinc-400 leading-relaxed mb-6">
            Punya proyek mendesak? Ingin chat langsung? Gunakan saluran di bawah ini untuk konsultasi instan.
          </p>

          <div class="flex flex-col gap-3">
            <a 
              href="https://wa.me/6282211110031" 
              target="_blank"
              class="flex items-center gap-3 p-3 bg-emerald-100 dark:bg-emerald-950/30 text-emerald-800 dark:text-emerald-400 border-2 border-black hover:translate-x-1 transition-transform font-bold"
            >
              <span>💬</span>
              <span>Hubungi via WhatsApp</span>
            </a>

            <a 
              href="https://github.com/tonimartinus" 
              target="_blank"
              class="flex items-center gap-3 p-3 bg-slate-100 dark:bg-zinc-800 text-black dark:text-white border-2 border-black hover:translate-x-1 transition-transform font-bold"
            >
              <span>💻</span>
              <span>Lihat Akun GitHub</span>
            </a>

            <a 
              href="https://linkedin.com" 
              target="_blank"
              class="flex items-center gap-3 p-3 bg-blue-100 dark:bg-blue-950/30 text-blue-800 dark:text-blue-400 border-2 border-black hover:translate-x-1 transition-transform font-bold"
            >
              <span>💼</span>
              <span>Hubungkan via LinkedIn</span>
            </a>

            <a 
              href="mailto:tonimartinuss@gmail.com" 
              class="flex items-center gap-3 p-3 bg-red-100 dark:bg-red-950/30 text-red-800 dark:text-red-400 border-2 border-black hover:translate-x-1 transition-transform font-bold"
            >
              <span>✉️</span>
              <span>Kirim Email Langsung</span>
            </a>
          </div>
        </div>

        <div class="p-4 bg-yellow-100 dark:bg-amber-950/20 border-2 border-amber-400 text-amber-900 dark:text-amber-400 text-xs leading-relaxed">
          <strong>⚠️ CATATAN SISTEM:</strong> Rata-rata waktu tanggapan pesan masuk adalah kurang dari 24 jam. Hari kerja aktif Senin s/d Sabtu.
        </div>
      </div>
    </div>
  </section>
</template>
