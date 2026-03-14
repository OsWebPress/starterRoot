<template>
  <pre class="text-blue-100"><MakedownInline :body="body" /></pre>
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
