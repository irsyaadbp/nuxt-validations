<script setup>
const isOpen = ref(false);
</script>

<template>
  <div>
    <div class="d-flex align-items-center gap-8">
      <button @click="isOpen = !isOpen">{{ isOpen ? "-" : "+" }}</button>
      <h4><slot name="title"></slot></h4>
    </div>
    <div v-show="isOpen">
      <slot> </slot>
    </div>
  </div>
</template>
