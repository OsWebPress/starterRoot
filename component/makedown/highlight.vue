<template>
  <code class="font-mono bg-amber-100 text-amber-900 px-1.5 py-0.5 rounded text-sm">{{ body }}<slot /></code>
</template>

<script setup>
defineProps({
  body: {
    type: String,
    default: ''
  }
});
</script>
