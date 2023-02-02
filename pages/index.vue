<script setup>
const listMenu = [
  { title: "Basic Example", url: "/basic-example" },
  { title: "Advance Validations", url: "/advance-validations" },
  { title: "Dynamic Form", url: "/dynamic-form" },
];
</script>

<template>
  <div class="container">
    <h2>Vee Validate</h2>
    <ul>
      <li v-for="(menu, index) in listMenu" :key="`menu-${index}`">
        <NuxtLink :to="menu.url">{{ menu.title }}</NuxtLink>
      </li>
    </ul>
  </div>
</template>
