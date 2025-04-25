<script setup>
import { ref } from 'vue';

const props = defineProps({
  navigationData: {
	type: Array,
	required: true,
  },
});

const navigation = ref(props.navigationData);
</script>

<template>
	<nav>
	  <ul>
		<li v-for="item in navigation" :key="item.url" :class="{ 'has-submenu': item.submenu }">
		  <router-link v-if="item.url" :to="item.url">
			<img v-if="item.image" :src="item.image" :alt="item.text">
			<span v-else>{{ item.text }}</span>
		  </router-link>
		  <span v-else>
			<img v-if="item.image" :src="item.image" :alt="item.text">
			<span v-else>{{ item.text }}</span>
		  </span>
		  <ul v-if="item.submenu" class="submenu">
			<li v-for="subItem in item.submenu" :key="subItem.url">
			  <router-link :to="subItem.url">
				{{ subItem.text }}
			  </router-link>
			  <ul v-if="subItem.submenu" class="submenu">
				<li v-for="nestedSubItem in subItem.submenu" :key="nestedSubItem.url">
				  <router-link :to="nestedSubItem.url">
					{{ nestedSubItem.text }}
				  </router-link>
				</li>
			  </ul>
			</li>
		  </ul>
		</li>
	  </ul>
	</nav>
  </template>

  <style scoped>
  /* ... (same CSS as before) ... */
  nav {
	background-color: #f0f0f0;
	margin: 0 0;
	padding: 15px 20px;
  }

  nav ul {
	list-style: none;
	padding: 0;
	margin: 0;
	display: flex;
  }

  nav li {
	margin-right: 20px;
	position: relative;
  }

  nav li:last-child {
	margin-right: 0;
  }

  nav a {
	text-decoration: none;
	color: #333;
	display: flex;
	align-items: center;
  }

  nav a img {
	height: 24px;
	margin-right: 8px;
	border-radius: 6px;
}


  .has-submenu > a::after {
	content: '▼';
	margin-left: 5px;
  }

  .submenu {
	list-style: none;
	padding: 0;
	margin: 0;
	position: absolute;
	top: 100%;
	left: 0;
	background-color: #fff;
	border: 1px solid #ccc;
	box-shadow: 2px 2px 5px rgba(0, 0, 0, 0.1);
	z-index: 10;
	display: none; /* Initially hidden */
  }

  .has-submenu:hover > .submenu {
	display: block;
  }

  .submenu li {
	margin: 0;
  }

  .submenu a {
	display: block;
	padding: 10px 15px;
	color: #333;
	white-space: nowrap;
  }

  .submenu a:hover {
	background-color: #eee;
  }

  /* Nested submenus */
  .submenu > li.has-submenu > a::after {
	content: '▶';
	float: right;
  }

  .submenu .submenu {
	left: 100%;
	top: 0;
  }

  .submenu > li.has-submenu:hover > .submenu {
	display: block;
  }
  </style>