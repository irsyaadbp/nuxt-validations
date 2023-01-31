<script setup>
import { reactive, onMounted } from "vue";
import { useVuelidate } from "@vuelidate/core";
import { required, numeric, email } from "@vuelidate/validators";

const getFields = () =>
  new Promise((resolve) => {
    const timeout = setTimeout(() => {
      resolve([
        {
          title: "Full Name",
          key: "full_name",
          type: "text",
          required: true,
        },
        {
          title: "Age",
          key: "age",
          type: "number",
          required: true,
        },
        {
          title: "email",
          key: "email",
          type: "email",
          required: true,
        },
      ]);
      clearTimeout(timeout);
    }, 500);
  });

const form = reactive({});
const fields = ref([]);

const rules = computed(() => {
  const validationsGroup = {};

  fields.value.forEach((field) => {
    const validations = {};
    if (field.required) validations.required = required;
    if (field.type === "email") validations.email = email;
    if (field.type === "number") validations.numeric = numeric;

    validationsGroup[field.key] = validations;
  });

  return validationsGroup;
});

const v$ = useVuelidate(rules, form, { $autoDirty: true });

/**
 * Function to submit form
 */
async function handleSubmit() {
  const isValidForm = await v$.value.$validate();

  if (!isValidForm) {
    console.log("invalid");
    return;
  }

  alert("SUBMIT FORM");
}

/**
 * Function to reset vuelidate
 */
function handleReset() {
  v$.value.$reset();
}

const load = async () => {
  try {
    const response = await getFields();

    fields.value = response;

    response.forEach((field) => {
      if (field.type === "number") {
        form[field.key] = 0;
        return;
      }

      form[field.key] = "";
    });
  } catch (error) {
    console.log({ error });
  }
};

onMounted(() => {
  load();
});
</script>

<template>
  <div class="card">
    <h4>Dynamic Field Example</h4>
    <hr />

    <div
      v-for="(field, index) in fields"
      class="form-group"
      :key="`field-${field.key}-${index}`"
    >
      <label for="fullName">{{ field.title }}</label>

      <input
        id="fullName"
        :type="field.type"
        v-model="form[field.key]"
        :class="{
          'error-field': v$[field.key].$invalid && v$[field.key].$dirty,
        }"
      />

      <p
        v-for="error in v$[field.key].$errors"
        :key="error.$uid"
        class="error-text"
      >
        <small>{{ error.$message }}</small>
      </p>
    </div>

    <div class="d-flex justify-content-end gap-8">
      <button @click="handleReset">Reset</button>
      <button @click="handleSubmit">Save</button>
    </div>
  </div>
</template>
