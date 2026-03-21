<template>
  <h4 class="font-['Josefin_Sans'] text-xl font-medium text-stone-700 mt-4 mb-2">
    <span class="text-amber-500 select-none"># </span><LoadComponent _component="makedown/richText" :body="body" />
  </h4>
</template>

<script setup>
defineProps({
  body: { type: String, default: '' }
});
</script>
