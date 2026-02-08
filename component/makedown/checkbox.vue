<template>
  <div class="flex items-center space-x-2">
    <input
      type="checkbox"
      :checked="checked"
      @change="$emit('update:checked', $event.target.checked)"
      class="w-5 h-5 text-blue-600 border-gray-300 rounded focus:ring-2 focus:ring-blue-500 cursor-pointer"
    />
    <label class="text-gray-700 cursor-pointer" @click="toggleCheck">
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
