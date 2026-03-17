<template>
  <h3 class="text-2xl md:text-3xl font-bold tracking-tight leading-tight text-cyan-200">
    <LoadComponent _component="makedown/richText" :body="body" />
  </h3>
</template>

<script setup>
defineProps({
  body: { type: String, default: '' }
});
</script>
