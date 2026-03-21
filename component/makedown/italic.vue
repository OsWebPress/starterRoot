<template>
  <em class="italic text-stone-600">{{ body }}<slot /></em>
</template>

<script setup>
defineProps({
  body: {
    type: String,
    default: ''
  }
});
</script>
