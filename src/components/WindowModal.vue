<script setup>
defineProps({
  title: {
    type: String,
    default: 'system.exe'
  },
  isOpen: {
    type: Boolean,
    required: true
  }
})

defineEmits(['close'])
</script>

<template>
  <div 
    v-if="isOpen"
    class="fixed inset-0 z-50 flex items-center justify-center p-4 bg-black/75 backdrop-blur-sm"
    @click.self="$emit('close')"
  >
    <div 
      class="w-full max-w-2xl bg-slate-100 dark:bg-[#1a1a1a] text-black dark:text-white neo-border neo-shadow animate-in fade-in zoom-in-95 duration-150"
      role="dialog"
      aria-modal="true"
    >
      <!-- Window Title Bar -->
      <div class="flex items-center justify-between bg-black text-white dark:bg-white dark:text-black p-2 font-mono text-sm uppercase font-bold border-b-4 border-black">
        <div class="flex items-center gap-2">
          <span>📟</span>
          <span>{{ title }}</span>
        </div>
        <div class="flex items-center gap-1">
          <button 
            class="px-2 py-0.5 border border-white dark:border-black text-xs hover:bg-zinc-800 dark:hover:bg-zinc-200 transition-colors"
            title="Minimize"
          >
            _
          </button>
          <button 
            class="px-2 py-0.5 border border-white dark:border-black text-xs hover:bg-zinc-800 dark:hover:bg-zinc-200 transition-colors mr-1"
            title="Maximize"
          >
            []
          </button>
          <button 
            class="px-2 py-0.5 bg-red-600 hover:bg-red-700 text-white font-bold border border-black text-xs transition-colors"
            @click="$emit('close')"
            title="Close"
          >
            X
          </button>
        </div>
      </div>
      
      <!-- Window Content -->
      <div class="p-6 overflow-y-auto max-h-[75vh]">
        <slot></slot>
      </div>
    </div>
  </div>
</template>
