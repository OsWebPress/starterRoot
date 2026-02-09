<script setup>
import { onBeforeUnmount } from 'vue'

const props = defineProps({
  title: {
    type: String,
    default: undefined
  },
  description: {
    type: String,
    default: ''
  },
  keywords: {
    type: String,
    default: ''
  },
  ogImage: {
    type: String,
    default: ''
  },
  ogType: {
    type: String,
    default: 'website'
  }
})

// Set page title
if (document.title !== undefined) {
  document.title = props.title
}

// Set or update meta tags
setMetaTag('description', props.description)
setMetaTag('keywords', props.keywords)

// Open Graph tags
setMetaTag('og:title', props.title, 'property')
setMetaTag('og:description', props.description, 'property')
setMetaTag('og:type', props.ogType, 'property')
if (props.ogImage) {
  setMetaTag('og:image', props.ogImage, 'property')
}

// Twitter Card tags
setMetaTag('twitter:card', 'summary_large_image', 'name')
setMetaTag('twitter:title', props.title, 'name')
setMetaTag('twitter:description', props.description, 'name')
if (props.ogImage) {
  setMetaTag('twitter:image', props.ogImage, 'name')
}

// Clear title and meta tags when component unmounts
onBeforeUnmount(() => {
  removeMetaTag('description')
  removeMetaTag('keywords')
  removeMetaTag('og:title', 'property')
  removeMetaTag('og:description', 'property')
  removeMetaTag('og:type', 'property')
  removeMetaTag('og:image', 'property')
  removeMetaTag('twitter:card', 'name')
  removeMetaTag('twitter:title', 'name')
  removeMetaTag('twitter:description', 'name')
  removeMetaTag('twitter:image', 'name')
})

function setMetaTag(key, content, attribute = 'name') {
  if (!content) return

  let element = document.querySelector(`meta[${attribute}="${key}"]`)

  if (element) {
    element.setAttribute('content', content)
  } else {
    element = document.createElement('meta')
    element.setAttribute(attribute, key)
    element.setAttribute('content', content)
    document.head.appendChild(element)
  }
}

function removeMetaTag(key, attribute = 'name') {
  const element = document.querySelector(`meta[${attribute}="${key}"]`)
  if (element) {
    element.remove()
  }
}
</script>