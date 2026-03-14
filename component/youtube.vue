<template>
  <div class="relative w-full aspect-video">
    <iframe
      v-if="embedUrl"
      :src="embedUrl"
      class="w-full h-full rounded-lg"
      title="YouTube video player"
      frameborder="0"
      allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share"
      referrerpolicy="strict-origin-when-cross-origin"
      allowfullscreen
    />
    <div v-else class="flex items-center justify-center w-full h-full bg-gray-100 rounded-lg text-gray-400">
      No valid YouTube URL provided
    </div>
  </div>
</template>

<script setup>
import { computed, useSlots } from 'vue'

const props = defineProps({
  url: {
    type: String,
    default: null,
  },
})

const slots = useSlots()

function extractVideoId(url) {
  if (!url) return null
  // Already an embed URL
  const embedMatch = url.match(/youtube\.com\/embed\/([a-zA-Z0-9_-]{11})/)
  if (embedMatch) return embedMatch[1]
  // Standard watch URL
  const watchMatch = url.match(/[?&]v=([a-zA-Z0-9_-]{11})/)
  if (watchMatch) return watchMatch[1]
  // Short URL youtu.be
  const shortMatch = url.match(/youtu\.be\/([a-zA-Z0-9_-]{11})/)
  if (shortMatch) return shortMatch[1]
  return null
}

function getSlotText() {
  if (!slots.default) return null
  const nodes = slots.default()
  for (const node of nodes) {
    const text = typeof node.children === 'string' ? node.children.trim() : null
    if (text) return text
  }
  return null
}

const embedUrl = computed(() => {
  const source = props.url || getSlotText()
  const videoId = extractVideoId(source)
  return videoId ? `https://www.youtube.com/embed/${videoId}` : null
})
</script>
