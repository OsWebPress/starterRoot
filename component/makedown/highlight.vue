<template>
  <code class="font-mono bg-yellow-200 px-1 rounded text-sm">{{ body }}<slot /></code>
</template>

<script setup>
defineProps({
  body: {
    type: String,
    default: ''
  }
});
</script>
