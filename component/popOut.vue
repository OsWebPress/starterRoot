<!-- Example component how to reverse the left marging to make a full width container and still respect the vertical spacing -->

<template>
  <div class="w-screen -ml-3rem md:-ml-6rem xl:-ml-12rem 2xl:-ml-18rem bg-gray-100 box-border">
    <slot></slot>
  </div>
</template>
