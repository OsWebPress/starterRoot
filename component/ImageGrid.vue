<template>
  <div class="w-screen -ml-3rem md:-ml-6rem xl:-ml-12rem 2xl:-ml-18rem bg-orange-100 box-border p-2">
    <div
      v-if="loading"
      class="flex items-center justify-center"
      style="min-height: 400px"
    >
      <span class="text-orange-400 text-sm animate-pulse">Loading images…</span>
    </div>

    <div
      v-else-if="error"
      class="flex items-center justify-center text-red-400 text-sm"
      style="min-height: 400px"
    >
      {{ error }}
    </div>

    <div
      v-else
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

<script setup>
import { computed, ref, watchEffect } from 'vue';

const IMAGE_EXTENSIONS = /\.(jpe?g|png|gif|webp|avif|svg|bmp|tiff?)(\?.*)?$/i;

const props = defineProps({
  body: {
    type: String,
    default: ''
  },
  directory: {
    type: String,
    default: ''
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

const loading = ref(false);
const error = ref('');
const directoryImages = ref([]);

const bodyImages = computed(() => {
  if (!props.body) return [];
  const imageRegex = /!\[([^\]]*)\]\(([^)]+)\)/g;
  const matches = [];
  let match;
  while ((match = imageRegex.exec(props.body)) !== null) {
    matches.push({ alt: match[1], src: match[2] });
  }
  return matches;
});

const images = computed(() => [
  ...bodyImages.value,
  ...directoryImages.value
]);

watchEffect(async () => {
  if (!props.directory) {
    directoryImages.value = [];
    return;
  }

  loading.value = true;
  error.value = '';

  try {
    const res = await fetch(props.directory);
    if (!res.ok) throw new Error(`Failed to fetch directory: ${res.status} ${res.statusText}`);

    const html = await res.text();
    const parser = new DOMParser();
    const doc = parser.parseFromString(html, 'text/html');
    const anchors = Array.from(doc.querySelectorAll('a[href]'));

    const base = props.directory.endsWith('/') ? props.directory : props.directory + '/';
    const absoluteBase = new URL(base, window.location.origin).href;

    directoryImages.value = anchors
      .map(a => a.getAttribute('href') || '')
      .filter(href => IMAGE_EXTENSIONS.test(href))
      .map(href => {
        const src = href.startsWith('http') ? href : new URL(href, absoluteBase).href;
        const alt = href.split('/').pop()?.replace(/\.[^.]+$/, '') || href;
        return { src, alt };
      });
  } catch (e) {
    error.value = e?.message || 'Unknown error loading directory';
    directoryImages.value = [];
  } finally {
    loading.value = false;
  }
});

const gridStyle = computed(() => ({
  gridTemplateColumns: `repeat(${props.width}, 1fr)`,
  gridTemplateRows: `repeat(${props.height}, 1fr)`,
  minHeight: '400px'
}));
</script>