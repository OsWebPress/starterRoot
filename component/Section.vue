<template>
  <LoadComponent _component="FullBleed">
    <div :class="large === 'true' ? 'relative min-h-screen' : 'relative'">

      <div
        v-if="bg"
        class="absolute inset-0"
        :class="bgClass"
        :style="bgStyle"
      />

      <div class="relative z-10 pl-3rem md:pl-6rem xl:pl-12rem 2xl:pl-18rem pr-8 max-w-4xl 2xl:max-w-6xl pt-12 pb-24">
        <Makedown :content="body" />
      </div>

    </div>
  </LoadComponent>
</template>

<script>
export default {
  name: 'Section',

  props: {
    bg: {
      type: String,
      default: '',
    },
    opacity: {
      type: String,
      default: '1',
    },
    body: {
      type: String,
      default: '',
    },
    large: {
      type: String,
      default: 'false',
    },
  },

  computed: {
    isCssColor() {
      return this.bg.startsWith('#') || this.bg.startsWith('rgb(') || this.bg.startsWith('hsl(')
    },
    bgClass() {
      if (!this.bg || this.isCssColor) return ''
      return `bg-${this.bg}`
    },
    bgStyle() {
      const style = { opacity: parseFloat(this.opacity) }
      if (this.isCssColor) style.backgroundColor = this.bg
      return style
    },
  },
}
</script>
