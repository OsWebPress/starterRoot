<template>
  <li class="text-gray-700 py-1 ml-5 list-decimal">
    <slot />
  </li>
</template>

<script setup>
const props = defineProps({
  number: {
    type: Number,
    required: false,
    default: 1
  }
})
console.log("OrderedListItem number:", props.number);
</script>