<template>
  <div class="form-group">
    <label v-if="label" :for="id">{{ label }}</label>
    <input
      v-model="vModel"
      :id="id"
      :class="{
        'error-field': !!errors.length,
      }"
    />

    <p
      v-for="(err, index) of errors"
      :key="`${err}-${index}`"
      class="error-text"
    >
      <small>{{ err }}</small>
    </p>
  </div>
</template>

<script setup lang="ts">
import { ErrorObject } from "@vuelidate/core";
import { PropType } from "nuxt/dist/app/compat/capi";

const props = defineProps({
  modelValue: {
    type: String,
    default: "",
  },
  label: {
    type: String,
    default: "",
  },
  id: {
    type: String,
    default: "input",
  },
  errorMessages: {
    type: [String, Array] as PropType<string | ErrorObject[]>,
    default: "",
  },
});

const { modelValue, errorMessages } = toRefs(props);

const emits = defineEmits(["update:modelValue"]);
const vModel = computed({
  get() {
    return modelValue.value;
  },
  set(value) {
    emits("update:modelValue", value);
  },
});

const errors = computed(() => {
  if (!errorMessages.value) return [];
  if (typeof errorMessages.value === "string") return [errorMessages.value];
  return errorMessages.value.map((item) => item.$message);
});
</script>

<style scoped></style>
