<template>
  <router-link
    v-if="isInternal"
    :to="url"
    class="text-amber-500 underline underline-offset-2 hover:text-amber-700 transition-colors"
  >
    {{ text }}
  </router-link>
  <a
    v-else
    :href="url"
    class="text-amber-500 underline underline-offset-2 hover:text-amber-700 transition-colors"
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
  },
  computed: {
    isInternal() {
      return this.url.startsWith('/');
    }
  }
}
</script>