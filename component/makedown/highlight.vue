<template>
  <code class="font-mono bg-amber-200 text-amber-900 px-1.5 py-0.5 rounded text-sm border border-amber-300">{{ body }}<slot /></code>
</template>

<script setup>
defineProps({
  body: {
    type: String,
    default: ''
  }
});
</script>
