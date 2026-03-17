<template>
  <LoadComponent _component="FullBleed"><div class="bg-orange-100 box-border p-2">
    <div class="grid gap-2 w-full h-full grid-cols-1 lg:grid-cols-3">
      <div
        v-for="(image, index) in images"
        :key="index"
        class="relative overflow-hidden rounded-lg shadow-lg bg-white max-h-[60vh]"
        :style="{ minHeight: (imageHeights[index] || 200) + 'px' }"
        :class="image.text && !flipped[index] ? 'cursor-pointer hover:ring-4 hover:ring-orange-400 hover:animate-pulse' : image.text ? 'cursor-pointer' : ''"
        @click="image.text ? (flipped[index] = !flipped[index]) : null"
      >
        <img
          v-if="!flipped[index]"
          :ref="el => { if (el) imgRefs[index] = el }"
          :src="image.src"
          :alt="image.alt"
          class="w-full h-full object-cover"
          @load="captureHeight(index)"
        />
        <div
          v-else
          class="relative w-full flex items-center justify-center p-6"
          :style="{ minHeight: (imageHeights[index] || 200) + 'px' }"
        >
          <div class="absolute inset-0 bg-white"></div>
          <img
            :src="image.src"
            :alt="image.alt"
            class="absolute inset-0 w-full h-full object-cover opacity-20"
          />
          <p class="relative text-gray-800 text-center text-sm leading-relaxed" v-html="parseMarkdown(image.text)"></p>
        </div>
      </div>
    </div>
  </div></LoadComponent>
</template>

<script setup>
import { ref, computed } from 'vue';

const props = defineProps({
  body: {
    type: String,
    required: true
  },
  height: {
    type: Number,
    default: 1
  }
});

const flipped = ref({});
const imgRefs = ref({});
const imageHeights = ref({});

function captureHeight(index) {
  const el = imgRefs.value[index];
  if (el) {
    imageHeights.value[index] = el.offsetHeight;
  }
}

function parseMarkdown(text) {
  if (!text) return '';
  return text
    .replace(/\*\*(.+?)\*\*/g, '<strong>$1</strong>')
    .replace(/\*(.+?)\*/g, '<em>$1</em>');
}

const images = computed(() => {
  const imageRegex = /!\[([^\]]*)\]\(([^)]+)\)(?:\(([^)]+)\))?/g;
  const matches = [];
  let match;
  while ((match = imageRegex.exec(props.body)) !== null) {
    matches.push({
      alt: match[1],
      src: match[2],
      text: match[3] || undefined
    });
  }
  return matches;
});
</script>