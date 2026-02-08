<template>
  <img
    :src="url"
    :alt="alt"
    class="max-w-full h-auto max-h-[50vh] rounded-lg"
  />
</template>

<script setup>

const props = defineProps({
  url: {
    type: String,
    required: true
  },
  alt: {
    type: String,
    default: ''
  }
});
</script>