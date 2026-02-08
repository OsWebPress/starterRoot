<template>
  <a
    :href="url"
    class="text-blue-600 hover:text-blue-800 underline hover:no-underline transition-colors"
    target="_blank"
    rel="noopener noreferrer"
  >
    {{ text }}
  </a>
</template>

<script>
export default {
  name: 'LinkComponent',
  props: {
    url: {
      type: String,
      default: 'https://example.com'
    },
    text: {
      type: String,
      default: 'Click here'
    }
  }
}
</script>