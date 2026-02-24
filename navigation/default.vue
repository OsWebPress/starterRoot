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
</script>
<template>
  <nav class="mx-0 px-5 py-[15px]">
    <ul class="list-none p-0 m-0 flex">
      <li
        v-for="item in navigation"
        :key="item.url"
        class="mr-5 last:mr-0 relative group"
      >
        <router-link
          v-if="item.url"
          :to="item.url"
          :class="[
            'no-underline flex items-center',
            item.url === props.path && !item.image ? 'text-red-500 underline' : 'text-[#333]'
          ]"
        >
          <img v-if="item.image" :src="item.image" :alt="item.text" :class="['h-6 mr-2 rounded-md', item.url === props.path ? 'border-2 border-red-500' : '']" />
          <span v-else>{{ item.text }}</span>
          <span v-if="item.submenu" class="ml-[5px]">▼</span>
        </router-link>
        <span
          v-else
          :class="[
            'flex items-center',
            item.url === props.path && !item.image ? 'text-red-500 underline' : 'text-[#333]'
          ]"
        >
          <img v-if="item.image" :src="item.image" :alt="item.text" :class="['h-6 mr-2 rounded-md', item.url === props.path ? 'border-2 border-red-500' : '']" />
          <span v-else>{{ item.text }}</span>
          <span v-if="item.submenu" class="ml-[5px]">▼</span>
        </span>
        <!-- Level 1 submenu -->
        <ul
          v-if="item.submenu"
          class="list-none p-0 m-0 absolute top-full left-0 bg-white border border-[#ccc] shadow-[2px_2px_5px_rgba(0,0,0,0.1)] z-10 hidden group-hover:block"
        >
          <li
            v-for="subItem in item.submenu"
            :key="subItem.url"
            class="m-0 relative group/sub"
          >
            <router-link
              :to="subItem.url"
              :class="[
                'block px-[15px] py-[10px] whitespace-nowrap no-underline hover:bg-[#eee] flex items-center',
                subItem.url === props.path && !subItem.image ? 'text-red-500 underline' : 'text-[#333]'
              ]"
            >
              <img v-if="subItem.image" :src="subItem.image" :alt="subItem.text" :class="['h-6 mr-2 rounded-md', subItem.url === props.path ? 'border-2 border-red-500' : '']" />
              <span v-else>{{ subItem.text }}</span>
              <span v-if="subItem.submenu" class="float-right ml-auto">▶</span>
            </router-link>
            <!-- Level 2 submenu -->
            <ul
              v-if="subItem.submenu"
              class="list-none p-0 m-0 absolute left-full top-0 bg-white border border-[#ccc] shadow-[2px_2px_5px_rgba(0,0,0,0.1)] z-10 hidden group-hover/sub:block"
            >
              <li
                v-for="nestedSubItem in subItem.submenu"
                :key="nestedSubItem.url"
                class="m-0"
              >
                <router-link
                  :to="nestedSubItem.url"
                  :class="[
                    'block px-[15px] py-[10px] whitespace-nowrap no-underline hover:bg-[#eee] flex items-center',
                    nestedSubItem.url === props.path && !nestedSubItem.image ? 'text-red-500 underline' : 'text-[#333]'
                  ]"
                >
                  <img v-if="nestedSubItem.image" :src="nestedSubItem.image" :alt="nestedSubItem.text" :class="['h-6 mr-2 rounded-md', nestedSubItem.url === props.path ? 'border-2 border-red-500' : '']" />
                  <span v-else>{{ nestedSubItem.text }}</span>
                </router-link>
              </li>
            </ul>
          </li>
        </ul>
      </li>
    </ul>
  </nav>
</template>
