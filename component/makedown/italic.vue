<template>
  <em class="italic">{{ body }}<slot /></em>
</template>

<script setup>
defineProps({
  body: {
    type: String,
    default: ''
  }
});
</script>
