<template>
  <div class="flex items-center space-x-2">
    <input
      type="checkbox"
      :checked="checked"
      @change="$emit('update:checked', $event.target.checked)"
      class="w-4 h-4 rounded-sm border-2 border-stone-400 accent-amber-500 cursor-pointer"
    />
    <label class="text-stone-700 cursor-pointer" @click="toggleCheck">
      <slot />
    </label>
  </div>
</template>

<script>
export default {
  name: 'CheckBox',
  props: {
    checked: {
      type: Boolean,
      default: false
		}
	}
//   ,
//   emits: ['update:checked'],
//   methods: {
//     toggleCheck() {
//       this.$emit('update:checked', !this.checked)
//     }
//   }
}
</script>
