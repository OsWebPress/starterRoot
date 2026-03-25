<template>
  <pre class="font-['JetBrains_Mono'] text-sm bg-gray-50 border border-gray-200 rounded-lg p-4 overflow-x-auto my-4 leading-relaxed"><code v-html="highlighted"></code></pre>
</template>

<script setup>
import { ref, onMounted } from 'vue'

const props = defineProps({
  body: { type: String, default: '' },
  lang: { type: String, default: '' },
});

const THEME_URL = 'https://cdnjs.cloudflare.com/ajax/libs/highlight.js/11.9.0/styles/atom-one-dark.min.css'
const HLJS_URL = 'https://cdnjs.cloudflare.com/ajax/libs/highlight.js/11.9.0/highlight.min.js'

const highlighted = ref(props.body)

let _hljs = null

const loadHljs = async () => {
  if (_hljs) return _hljs
  const code = await fetch(HLJS_URL).then(r => r.text())
  _hljs = new Function('var define=undefined;\n' + code + '\nreturn hljs;')()
  return _hljs
}

onMounted(async () => {
  if (!document.querySelector(`link[href="${THEME_URL}"]`)) {
    const link = document.createElement('link')
    link.rel = 'stylesheet'
    link.href = THEME_URL
    document.head.appendChild(link)
  }

  const hljs = await loadHljs()
  try {
    highlighted.value = props.lang
      ? hljs.highlight(props.body, { language: props.lang }).value
      : hljs.highlightAuto(props.body).value
  } catch {
    highlighted.value = hljs.highlightAuto(props.body).value
  }
})
</script>
