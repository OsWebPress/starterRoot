<template>
  <blockquote class="border-l-4 border-amber-400 bg-amber-50 pl-4 py-2 my-4 italic text-stone-600 rounded-r">
    <LoadComponent _component="makedown/richText" :body="body" />
  </blockquote>
</template>

<script setup>
defineProps({
  body: { type: String, default: '' }
});
</script>
