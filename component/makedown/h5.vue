<template>
  <h5 class="text-lg md:text-xl font-bold tracking-tight leading-tight text-cyan-200">
    <LoadComponent _component="makedown/richText" :body="body" />
  </h5>
</template>

<script setup>
defineProps({
  body: { type: String, default: '' }
});
</script>
