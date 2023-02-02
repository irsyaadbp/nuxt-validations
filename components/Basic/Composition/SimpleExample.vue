<script setup>
import { useField } from "vee-validate";

function validateField(value) {
  if (!value) {
    return "this field is required";
  }

  if (value.length < 8) {
    return "this field must contain at least 8 characters";
  }

  return true;
}

const { value, errorMessage, meta, handleReset } = useField(
  "fullName",
  validateField
);

function submit() {
  if (!meta.valid) {
    console.log("Still has error field");
    return;
  }
  alert("Submit Form");
}
</script>

<template>
  <div class="card">
    <h4>Simple Example</h4>
    <hr />
    <pre>{{ meta }}</pre>
    <form @submit.prevent="submit">
      <div class="form-group">
        <input
          v-model="value"
          placeholder="Type something"
          :class="{ 'error-field': !!errorMessage }"
        />
        <span class="error-text">{{ errorMessage }}</span>
      </div>

      <button type="button" @click="handleReset">Reset</button>
      <button type="submit" :disabled="!meta.dirty">Submit</button>
    </form>
  </div>
</template>
