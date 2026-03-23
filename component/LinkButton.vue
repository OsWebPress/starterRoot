<template>
  <router-link
    v-if="isInternal"
    :to="href"
    class="inline-block bg-amber-500 hover:bg-amber-600 text-amber-50 text-sm font-medium px-4 py-2 rounded transition-colors no-underline"
  >
    <slot />
  </router-link>
  <a
    v-else
    :href="href"
    class="inline-block bg-amber-500 hover:bg-amber-600 text-amber-50 text-sm font-medium px-4 py-2 rounded transition-colors no-underline"
  >
    <slot />
  </a>
</template>

<script setup>
import { computed } from 'vue';

const props = defineProps({
  href: { type: String, required: true }
});

const isInternal = computed(() => props.href.startsWith('/'));
</script>
