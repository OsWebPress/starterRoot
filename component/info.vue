<template>
  <div class="my-2 flex flex-col rounded-lg bg-green-100 p-2">
    <div class="flex items-center">
      <span class="ml-1.5 rounded px-1.6 py-0.8 text-base font-semibold text-green-500">
        Tip:
      </span>
    </div>
    <div class="mt-1 rounded-md bg-white/50 p-2 text-green-700">
      <slot></slot>
    </div>
  </div>
</template>

<script setup>
// Purely presentational component
</script>