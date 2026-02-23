<template>
<div><img
    :src="url"
    :alt="alt"
    class="w-full h-full object-cover fixed top-0 left-0 -z-10"
/></div>
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