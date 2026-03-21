<template>
  <li class="text-stone-700 py-1 ml-6 list-decimal marker:text-amber-700">
    <LoadComponent _component="makedown/richText" :body="body" />
  </li>
</template>

<script setup>
defineProps({
  body: { type: String, default: '' }
});
</script>
