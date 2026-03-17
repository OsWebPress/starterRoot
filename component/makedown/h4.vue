<template>
  <h4 class="text-xl md:text-2xl font-bold tracking-tight leading-tight text-cyan-200">
    <LoadComponent _component="makedown/richText" :body="body" />
  </h4>
</template>

<script setup>
defineProps({
  body: { type: String, default: '' }
});
</script>
