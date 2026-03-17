<template>
  <h6 class="text-base md:text-lg font-bold tracking-tight leading-tight text-cyan-200">
    <LoadComponent _component="makedown/richText" :body="body" />
  </h6>
</template>

<script setup>
defineProps({
  body: { type: String, default: '' }
});
</script>
