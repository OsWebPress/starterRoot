<template>
  <div class="w-screen -ml-3rem md:-ml-6rem xl:-ml-12rem 2xl:-ml-18rem bg-orange-100 box-border p-2">
    <div
      class="grid gap-2 w-full h-full"
      :style="gridStyle"
    >
      <div
        v-for="(image, index) in images"
        :key="index"
        class="relative overflow-hidden rounded-lg shadow-lg bg-white max-h-[60vh]"
      >
        <img
          :src="image.src"
          :alt="image.alt"
          class="w-full h-full object-cover"
        />
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { computed } from 'vue';

const props = defineProps({
  body: {
    type: String,
    required: true
  },
  width: {
    type: Number,
    default: 2
  },
  height: {
	type: Number,
	default: 1
  }
});

// Parse markdown images from the body content
const images = computed(() => {
  const imageRegex = /!\[([^\]]*)\]\(([^)]+)\)/g;
  const matches = [];
  let match;

  while ((match = imageRegex.exec(props.body)) !== null) {
    matches.push({
      alt: match[1],
      src: match[2]
    });
  }

  return matches;
});

// Generate dynamic grid style based on x and y props
const gridStyle = computed(() => {
  return {
    gridTemplateColumns: `repeat(${props.width}, 1fr)`,
    gridTemplateRows: `repeat(${props.height}, 1fr)`,
    minHeight: '400px' // Adjust as needed
  };
});
</script>