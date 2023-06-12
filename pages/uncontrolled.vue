<template>
  <div class="container">
    <form @submit.prevent="handleSubmit">
      <div class="form-group">
        <input name="firstName" />
      </div>
      <div class="form-group">
        <input name="lastName" />
      </div>
      <button>Save</button>
    </form>
  </div>
</template>

<script setup lang="ts">
function handleSubmit(event) {
  console.log(event.target);
  const formData = new FormData(event.target);
}
</script>

<style scoped></style>
