<template>
  <h3 class="font-['Josefin_Sans'] text-2xl font-semibold text-stone-800 mt-5 mb-3">
    <span class="text-amber-500 select-none"># </span><LoadComponent _component="makedown/richText" :body="body" />
  </h3>
</template>

<script setup>
defineProps({
  body: { type: String, default: '' }
});
</script>
