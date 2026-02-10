<!-- <template>
  <div class="w-screen -ml-24 bg-orange-100 box-border">
    {{ props.body }}, x: "{{ props.x }}", y: "{{ props.y }}"

  </div>
</template>
<script setup lang="ts">
const props = defineProps({
  body: {
	type: String
	},
	x: {
	type: Number
	},
	y: {
	type: Number
	}
});
</script> -->

<template>
  <div class="w-screen -ml-24 bg-orange-100 box-border p-4">
    <div
      class="grid gap-4 w-full h-full"
      :style="gridStyle"
    >
      <div
        v-for="(image, index) in images"
        :key="index"
        class="relative overflow-hidden rounded-lg shadow-lg bg-white"
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
  x: {
    type: Number,
    default: 2
  },
  y: {
    type: Number,
    default: 2
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
    gridTemplateColumns: `repeat(${props.x}, 1fr)`,
    gridTemplateRows: `repeat(${props.y}, 1fr)`,
    minHeight: '400px' // Adjust as needed
  };
});
</script>