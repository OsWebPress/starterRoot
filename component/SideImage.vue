<template>
  <div class="w-screen -ml-3rem md:-ml-6rem xl:-ml-12rem 2xl:-ml-18rem">
    <!-- Large screens: side by side -->
    <div class="hidden lg:flex">
      <div class="w-[40%]">
        <img :src="image" alt="" class="w-full h-full object-cover" />
      </div>
      <div class="w-[60%] flex items-center justify-center p-8 bg-white opacity-80">
        <div class="text-gray-800 text-sm leading-relaxed" v-html="parsedContent"></div>
      </div>
    </div>

    <!-- Small screens: stacked -->
    <div class="flex flex-col lg:hidden">
      <div class="max-h-[60vh] overflow-hidden">
        <img :src="image" alt="" class="w-full h-full object-cover" />
      </div>
      <div class="p-6bg-white bg-white opacity-80">
        <div class="text-gray-800 text-sm leading-relaxed" v-html="parsedContent"></div>
        <Info>info</Info>
        <MakedownInline body="**boldie**">**bold**</MakedownInline>
      </div>
    </div>
  </div>
</template>

<script setup>
import { computed } from 'vue';

const props = defineProps({
  image: {
    type: String,
    required: true
  },
  body: {
    type: String,
    required: true
  }
});

function parseMarkdown(text) {
  if (!text) return '';
  return text
    .replace(/\*\*(.+?)\*\*/g, '<strong>$1</strong>')
    .replace(/\*(.+?)\*/g, '<em>$1</em>')
	.replace(/# (.+?)\n/g, '<h1 class="text-4xl font-bold mb-4 text-cyan-700">$1</h1>')
	.replace(/## (.+?)\n/g, '<h2 class="text-2xl font-bold mb-2">$1</h2>')
	.replace(/\n/g, '<br>')
}

const parsedContent = computed(() => parseMarkdown(props.body));
</script>