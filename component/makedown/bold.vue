<template>
  <strong class="font-bold">{{ body }}<slot /></strong>
</template>

<script setup>
defineProps({
  body: {
    type: String,
    default: ''
  }
});
</script>
