<template>
  <blockquote class="border-l-4 border-cyan-300 pl-4 py-2 italic text-blue-100 bg-black/25">
    <LoadComponent _component="makedown/richText" :body="body" />
  </blockquote>
</template>

<script setup>
defineProps({
  body: { type: String, default: '' }
});
</script>
