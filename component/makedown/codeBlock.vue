<template>
  <pre class="font-['JetBrains_Mono'] text-sm bg-stone-800 text-amber-100 rounded-lg p-4 overflow-x-auto my-4 leading-relaxed"><code>{{ body }}</code></pre>
</template>

<script setup>
defineProps({
  body: { type: String, default: '' }
});
</script>
