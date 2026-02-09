<template>
  <div class="text-black" v-html="processedText"></div>
</template>

<script setup>
import { computed } from 'vue';

function escapeHtml(unsafe) {
  return unsafe
    .replace(/&/g, "&amp;")
    .replace(/</g, "&lt;")
    .replace(/>/g, "&gt;")
    .replace(/"/g, "&quot;")
    .replace(/'/g, "&#039;");
}

const props = defineProps({
  body: {
    type: String,
    required: true,
    default: ""
  }
});

const processedText = computed(() => {
  let text = escapeHtml(props.body);

  // Highlight: `text`
  text = text.replace(/`([^`]+)`/g, '<span class="bg-yellow-200 text-gray-800 px-1 rounded">$1</span>');

  // Bold: **text** or __text__
  text = text.replace(/(\*\*|__)(.*?)\1/g, '<strong>$2</strong>');
  // Italic: *text* or _text_
  text = text.replace(/(\*|_)(.*?)\1/g, '<em>$2</em>');

  return text;
});
</script>