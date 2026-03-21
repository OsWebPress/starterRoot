<template>
  <h5 class="font-['Josefin_Sans'] text-lg font-medium text-stone-600 mt-3 mb-2">
    <span class="text-amber-500 select-none"># </span><LoadComponent _component="makedown/richText" :body="body" />
  </h5>
</template>

<script setup>
defineProps({
  body: { type: String, default: '' }
});
</script>
