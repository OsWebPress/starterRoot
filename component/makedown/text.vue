<template>
  <span class="text-blue-400 whitespace-pre-wrap overflow-x-auto">
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
