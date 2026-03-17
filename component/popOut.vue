<!-- Example component how to reverse the left margin to make a full width container and still respect the vertical spacing -->

<template>
  <LoadComponent _component="FullBleed">
    <div class="bg-gray-100 box-border">
      <slot></slot>
    </div>
  </LoadComponent>
</template>
