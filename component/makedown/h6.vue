<template>
  <h6 class="font-['Josefin_Sans'] text-base font-medium text-stone-500 mt-3 mb-1">
    <span class="text-amber-500 select-none"># </span><LoadComponent _component="makedown/richText" :body="body" />
  </h6>
</template>

<script setup>
defineProps({
  body: { type: String, default: '' }
});
</script>
