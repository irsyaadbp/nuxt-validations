<script setup>
import { useField } from "vee-validate";

const props = defineProps({
  name: { type: String, required: true },
});
const { value, errorMessage } = useField(props.name);
</script>

<template>
  <div class="form-group">
    <input
      v-model="value"
      :name="props.name"
      placeholder="Type something"
      :class="{ 'error-field': !!errorMessage }"
    />
    <span class="error-text">{{ errorMessage }}</span>
  </div>
</template>
