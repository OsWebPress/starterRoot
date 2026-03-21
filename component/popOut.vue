<!-- Example component how to reverse the left margin to make a full width container and still respect the vertical spacing -->

<template>
  <LoadComponent _component="FullBleed">
    <div class="bg-amber-50 border-l-4 border-amber-400 shadow-sm p-4 text-stone-700">
      <slot></slot>
    </div>
  </LoadComponent>
</template>
