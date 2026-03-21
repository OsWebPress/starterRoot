<template>
  <h1 class="font-['Josefin_Sans'] text-4xl font-bold tracking-tight leading-tight text-stone-800 mt-8 mb-6">
    <span class="text-amber-500 select-none"># </span><LoadComponent _component="makedown/richText" :body="body" />
  </h1>
</template>

<script setup>
defineProps({
  body: { type: String, default: '' }
});
</script>
