<script setup lang="ts">
import { PropType } from "nuxt/dist/app/compat/capi";
import { useField } from "vee-validate";
const props = defineProps({
  name: {
    type: String,
    default: "",
  },
  type: {
    type: String as PropType<"text" | "image">,
    default: "text",
  },
});
const { value, errorMessage } = useField(props.name);
const typeInput = computed(() => (props.type === "image" ? "file" : "text"));
</script>
<template>
  <div>
    <input :type="typeInput" />
    <p>
      <small v-if="errorMessage" class="error-text">{{ errorMessage }}</small>
    </p>
  </div>
</template>

<style scoped></style>
