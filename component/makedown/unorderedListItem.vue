<template>
  <div><li class="text-stone-700 py-1 ml-6 list-disc marker:text-amber-500">
    <LoadComponent _component="makedown/richText" :body="body" />
  </li></div>
</template>

<script setup>
defineProps({
  body: { type: String, default: '' }
});
</script>
