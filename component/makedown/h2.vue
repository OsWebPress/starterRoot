<template>
  <h2 class="text-3xl md:text-4xl font-bold tracking-tight leading-tight text-cyan-200">
    <LoadComponent _component="makedown/richText" :body="body" />
  </h2>
</template>

<script setup>
defineProps({
  body: { type: String, default: '' }
});
</script>
