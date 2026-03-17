<template>
  <div>
    <div v-if="loading" class="text-sm text-stone-400 animate-pulse py-8">Loading posts…</div>

    <div v-else-if="error" class="text-sm text-red-400 py-8">{{ error }}</div>

    <div v-else-if="posts.length === 0" class="text-sm text-stone-400 py-8">No posts found.</div>

    <div v-else class="grid gap-4 sm:grid-cols-2 lg:grid-cols-3">
      <LoadComponent
        v-for="post in posts"
        :key="post.href"
        _component="BlogPreview"
        :title="post.title"
        :date="post.date"
        :excerpt="post.excerpt"
        :href="post.href"
      />
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'

const props = defineProps({
  slug: {
    type: String,
    default: 'carbon/blog',
  },
  limit: {
    type: Number,
    default: 10,
  },
})

const loading = ref(true)
const error = ref('')
const posts = ref([])

function parsePost(content, filename) {
  const lines = content.split('\n')

  const titleLine = lines.find(l => l.startsWith('# '))
  const title = titleLine
    ? titleLine.replace(/^# /, '').trim()
    : filename.replace(/\.md$/, '').replace(/^\d{4}-\d{2}-\d{2}-/, '')

  const dateMatch = filename.match(/^(\d{4}-\d{2}-\d{2})/)
  const date = dateMatch ? dateMatch[1] : ''

  const excerpt = lines.find(l => l.trim() && !l.startsWith('#') && !l.startsWith('---')) || ''

  const basePath = props.slug.replace(/^carbon\//, '')
  const href = `/${basePath}/${filename.replace(/\.md$/, '')}`

  return { title, date, excerpt: excerpt.trim(), href }
}

onMounted(async () => {
  try {
    const listRes = await fetch(`/api/${props.slug}/`)
    if (!listRes.ok) throw new Error(`Could not list posts (${listRes.status})`)

    const html = await listRes.text()
    const doc = new DOMParser().parseFromString(html, 'text/html')
    const filenames = Array.from(doc.querySelectorAll('a[href]'))
      .map(a => a.getAttribute('href') || '')
      .filter(href => href.endsWith('.md'))
      .map(href => href.split('/').pop())
      .filter(Boolean)
      .sort()
      .reverse()
      .slice(0, props.limit)

    const fetched = await Promise.all(
      filenames.map(async filename => {
        const res = await fetch(`/api/${props.slug}/${filename}`)
        if (!res.ok) return null
        const content = await res.text()
        return parsePost(content, filename)
      })
    )

    posts.value = fetched.filter(Boolean)
  } catch (e) {
    error.value = e?.message || 'Failed to load posts'
  } finally {
    loading.value = false
  }
})
</script>
