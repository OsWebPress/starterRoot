<script setup>
import { ref } from 'vue';
const props = defineProps({
  navigationData: {
    type: Array,
    required: true,
  },
  path: {
    type: String,
    required: false,
  },
});
const navigation = ref(props.navigationData);
const mobileOpen = ref(false);
</script>

<template>
  <nav class="bg-amber-100 border-b-2 border-amber-300">
    <div class="pl-3rem md:pl-6rem xl:pl-12rem 2xl:pl-18rem pr-8 max-w-4xl 2xl:max-w-6xl h-14 flex items-center justify-between">

      <!-- Logo -->
      <router-link to="/" class="no-underline flex items-center" aria-label="indented.dev home">
        <svg viewBox="0 0 48 24" width="48" height="24" fill="none" xmlns="http://www.w3.org/2000/svg">
          <rect x="8" y="2" width="22" height="6" rx="2" fill="#3b82f6"/>
          <rect x="16" y="16" width="22" height="6" rx="2" fill="#3b82f6"/>
        </svg>
      </router-link>

      <!-- Desktop links -->
      <ul class="hidden md:flex items-center gap-6 list-none m-0 p-0">
        <li
          v-for="item in navigation"
          :key="item.url"
          class="relative group"
        >
          <router-link
            v-if="item.url"
            :to="item.url"
            :class="[
              'text-sm font-medium no-underline transition-colors',
              item.url === props.path
                ? 'text-amber-600 border-b-2 border-amber-500 pb-0.5'
                : 'text-stone-700 hover:text-amber-600'
            ]"
          >
            {{ item.text }}
          </router-link>

          <!-- Dropdown submenu -->
          <ul
            v-if="item.submenu"
            class="absolute top-full left-0 mt-1 bg-amber-50 border border-amber-200 shadow-md rounded-lg list-none p-1 min-w-max hidden group-hover:block z-10"
          >
            <li v-for="subItem in item.submenu" :key="subItem.url">
              <router-link
                :to="subItem.url"
                :class="[
                  'block px-4 py-2 text-sm rounded no-underline transition-colors',
                  subItem.url === props.path
                    ? 'text-amber-600'
                    : 'text-stone-700 hover:text-amber-600 hover:bg-amber-100'
                ]"
              >
                {{ subItem.text }}
              </router-link>
            </li>
          </ul>
        </li>
      </ul>

      <!-- Hamburger button -->
      <button
        class="md:hidden flex flex-col justify-center gap-1.5 w-8 h-8 p-1 text-stone-700 cursor-pointer bg-transparent border-0"
        @click="mobileOpen = !mobileOpen"
        aria-label="Toggle menu"
      >
        <span class="block w-full h-0.5 bg-stone-700 transition-all duration-200 origin-center" :class="mobileOpen ? 'rotate-45 translate-y-2' : ''" />
        <span class="block w-full h-0.5 bg-stone-700 transition-all duration-200" :class="mobileOpen ? 'opacity-0' : ''" />
        <span class="block w-full h-0.5 bg-stone-700 transition-all duration-200 origin-center" :class="mobileOpen ? '-rotate-45 -translate-y-2' : ''" />
      </button>
    </div>

    <!-- Mobile drawer -->
    <div v-if="mobileOpen" class="md:hidden border-t border-amber-200">
      <ul class="pl-3rem md:pl-6rem list-none m-0 p-0">
        <li v-for="item in navigation" :key="item.url">
          <router-link
            v-if="item.url"
            :to="item.url"
            :class="[
              'block py-3 px-6 text-sm font-medium no-underline transition-colors',
              item.url === props.path
                ? 'text-amber-600 border-l-2 border-amber-500 bg-amber-50'
                : 'text-stone-700 hover:text-amber-600 hover:bg-amber-50'
            ]"
            @click="mobileOpen = false"
          >
            {{ item.text }}
          </router-link>
        </li>
      </ul>
    </div>
  </nav>
</template>
