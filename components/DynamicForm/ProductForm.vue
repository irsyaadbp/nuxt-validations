<script setup>
import { useVuelidate } from "@vuelidate/core";
import { minValue, required, numeric } from "@vuelidate/validators";

const props = defineProps({
  modelValue: {
    type: Object,
    default: () => ({}),
  },
  disabledDelete: {
    type: Boolean,
    default: false,
  },
});

const emit = defineEmits(["update:modelValue", "delete"]);

const vModel = computed({
  get() {
    return props.modelValue;
  },
  set(value) {
    console.log({ value });
    emit("update:modelValue", value);
  },
});

const rules = {
  name: { required },
  qty: { required, numeric, minValue: minValue(1) },
};

const v$ = useVuelidate(rules, vModel, { $autoDirty: true });
</script>

<template>
  <div class="d-flex gap-8" style="margin-bottom: 16px">
    <div class="form-group">
      <label for="productName">Product Name</label>

      <input
        id="productName"
        type="text"
        v-model="vModel.name"
        :class="{ 'error-field': v$.name.$invalid && v$.name.$dirty }"
      />

      <p v-for="error in v$.name.$errors" :key="error.$uid" class="error-text">
        <small>{{ error.$message }}</small>
      </p>
    </div>

    <div class="form-group">
      <label for="qty">Quantity</label>

      <input
        id="qty"
        type="number"
        v-model="vModel.qty"
        :class="{ 'error-field': v$.qty.$invalid && v$.qty.$dirty }"
      />

      <p v-for="error in v$.qty.$errors" :key="error.$uid" class="error-text">
        <small>{{ error.$message }}</small>
      </p>
    </div>
    <button
      style="align-self: center"
      @click="$emit('delete', index)"
      :disabled="disabledDelete"
    >
      Delete
    </button>
  </div>
</template>
