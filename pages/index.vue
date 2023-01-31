<script setup>
const listMenu = [
  { title: "Basic Example", url: "/basic-example" },
  { title: "Custom Error Message", url: "/custom-error-messages" },
  { title: "Custom Validations", url: "/custom-validations" },
  { title: "Dynamic Form", url: "/dynamic-form" },
];
</script>

<template>
  <div class="container">
    <h2>Vuelidate</h2>
    <ul>
      <li v-for="(menu, index) in listMenu" :key="`menu-${index}`">
        <NuxtLink :to="menu.url">{{ menu.title }}</NuxtLink>
      </li>
    </ul>
  </div>
</template>

