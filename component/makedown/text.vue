<template>
  <span class="text-stone-700 leading-relaxed whitespace-pre-wrap">
    <LoadComponent _component="makedown/richText" :body="body" />
  </span>
</template>

<script setup>
const props = defineProps({
  body: {
    type: String,
    required: true,
    default: ""
  }
});
</script>
