<template>
<LoadComponent _component="FullBleed">
  <div class="flex items-start bg-stone-50 border border-stone-200 overflow-hidden shadow-sm min-h-[220px]">

    <!-- Left spacing accent: 1/16th width -->
    <div class="w-[6.25%] self-stretch bg-gradient-to-b from-amber-300 to-amber-600 shrink-0 min-w-[12px]" />

    <!-- Image -->
    <div class="shrink-0 p-5 pl-5">
      <img :src="image" alt="Content image" class="w-40 h-40 object-cover rounded-lg shadow-md block" />
    </div>

    <!-- Body text with markdown rendering -->
    <div class="flex-1 py-6 px-7 text-stone-700 leading-relaxed prose-body" v-html="renderedBody" />

  </div>
</LoadComponent>
</template>

<script>
export default {
  name: 'ContentCard',

  props: {
    image: {
      type: String,
      required: true,
    },
    body: {
      type: String,
      required: true,
    },
  },

  computed: {
    renderedBody() {
      console.log(this.body)
      return this.parseMarkdown(this.body)
    },
  },

  methods: {
    parseMarkdown(text) {
      // Escape raw HTML first for safety
      let html = text
        .replace(/&/g, '&amp;')
        .replace(/</g, '&lt;')
        .replace(/>/g, '&gt;')

      // Headers (must come before inline rules)
      html = html.replace(/^### (.+)$/gm, '<h3 class="text-base font-semibold uppercase tracking-widest text-amber-700 mb-2">$1</h3>')
      html = html.replace(/^## (.+)$/gm, '<h2 class="text-xl font-semibold text-stone-800 mb-2 tracking-tight">$1</h2>')
      html = html.replace(/^# (.+)$/gm,  '<h1 class="text-2xl font-bold text-stone-900 mb-3 tracking-tight leading-tight">$1</h1>')

      // Bold
      html = html.replace(/\*\*(.+?)\*\*/g, '<strong class="font-semibold text-stone-900">$1</strong>')

      // Italic
      html = html.replace(/\*(.+?)\*/g, '<em class="italic text-stone-600">$1</em>')

      // Highlight / inline code (backticks)
      html = html.replace(/`(.+?)`/g, '<mark class="bg-amber-100 text-amber-800 px-1.5 py-0.5 rounded font-mono text-sm not-italic">$1</mark>')

      // Paragraphs: wrap non-header lines in <p> tags
      html = html
        .split('\n')
        .map(line => {
          const trimmed = line.trim()
          if (!trimmed) return ''
          if (/^<h[123]/.test(trimmed)) return trimmed
          return `<p class="text-sm font-light text-stone-600 mb-2 last:mb-0">${trimmed}</p>`
        })
        .filter(line => line !== '')
        .join('\n')

      return html
    },
  },
}
</script>