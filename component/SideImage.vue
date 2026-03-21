<template>
  <LoadComponent _component="FullBleed">
    <!-- Large screens: side by side -->
    <div class="hidden lg:flex">
      <div class="w-[40%]">
        <img :src="image" alt="" class="w-full h-full object-cover" />
      </div>
      <div class="w-[60%] flex items-center justify-center p-8 bg-amber-50">
        <div class="text-stone-700 text-base leading-relaxed w-full min-w-0">
          <Makedown :content="body" />
        </div>
      </div>
    </div>

    <!-- Small screens: stacked -->
    <div class="flex flex-col lg:hidden">
      <div class="max-h-[60vh] overflow-hidden">
        <img :src="image" alt="" class="w-full h-full object-cover" />
      </div>
      <div class="p-6 bg-amber-50">
        <div class="text-stone-700 text-base leading-relaxed">
          <Makedown :content="body" />
        </div>
      </div>
    </div>
  </LoadComponent>
</template>

<script setup>
const props = defineProps({
  image: {
    type: String,
    required: true
  },
  body: {
    type: String,
    required: true
  }
});
</script>
