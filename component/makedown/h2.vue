<template>
  <h2 class="font-['Josefin_Sans'] text-3xl font-semibold tracking-tight leading-tight text-stone-800 mt-6 mb-4">
    <span class="text-amber-500 select-none"># </span><LoadComponent _component="makedown/richText" :body="body" />
  </h2>
</template>

<script setup>
defineProps({
  body: { type: String, default: '' }
});
</script>
