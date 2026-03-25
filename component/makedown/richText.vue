<template>
  <template v-for="(seg, i) in segments" :key="i">
    <LoadComponent v-if="seg.type !== 'text'" :_component="`makedown/${seg.type}`" :body="seg.content" :text="seg.content" :url="seg.url" />
    <span v-else>{{ seg.content }}</span>
  </template>
</template>

<script setup>
import { computed } from 'vue';

const props = defineProps({
  body: {
    type: String,
    default: ''
  }
});

const segments = computed(() => {
  const result = [];
  const regex = /\*\*(.+?)\*\*|\*([^*]+)\*|`([^`]+)`|\[(.+?)\]\(([^)]+)\)/g;
  let last = 0;
  let m;

  while ((m = regex.exec(props.body)) !== null) {
    if (m.index > last) {
      result.push({ type: 'text', content: props.body.slice(last, m.index) });
    }
    if (m[1] !== undefined) result.push({ type: 'bold', content: m[1] });
    else if (m[2] !== undefined) result.push({ type: 'italic', content: m[2] });
    else if (m[3] !== undefined) result.push({ type: 'highlight', content: m[3] });
    else if (m[4] !== undefined) result.push({ type: 'link', content: m[4], url: m[5] });
    last = m.index + m[0].length;
  }

  if (last < props.body.length) {
    result.push({ type: 'text', content: props.body.slice(last) });
  }

  return result;
});
</script>

