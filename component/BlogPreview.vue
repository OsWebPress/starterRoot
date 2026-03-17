<template>
  <a :href="href" class="block group border border-stone-200 bg-stone-50 hover:bg-white hover:shadow-md transition-all duration-200 p-6 rounded-sm">
    <div class="flex items-center gap-3 mb-3">
      <span v-if="date" class="text-xs font-mono text-amber-700 bg-amber-50 border border-amber-200 px-2 py-0.5 rounded">{{ date }}</span>
    </div>
    <h2 class="text-lg font-semibold text-stone-800 group-hover:text-amber-700 transition-colors mb-2 leading-snug">{{ title }}</h2>
    <p class="text-sm text-stone-500 leading-relaxed line-clamp-3 mb-4">{{ excerpt }}</p>
    <span class="text-xs font-medium text-amber-600 group-hover:text-amber-800 transition-colors">Read on →</span>
  </a>
</template>

<script setup>
defineProps({
  title: {
    type: String,
    required: true,
  },
  date: {
    type: String,
    default: '',
  },
  excerpt: {
    type: String,
    default: '',
  },
  href: {
    type: String,
    required: true,
  },
})
</script>
