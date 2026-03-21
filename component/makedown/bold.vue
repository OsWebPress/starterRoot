<template>
  <strong class="font-semibold text-stone-800">{{ body }}<slot /></strong>
</template>

<script setup>
defineProps({
  body: {
    type: String,
    default: ''
  }
});
</script>
