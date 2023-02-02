<script setup>
import { ErrorMessage, Field, Form } from "vee-validate";
import * as yup from "yup";
const fields = ref([
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
    title: "Email",
    key: "email",
    type: "email",
    required: true,
  },
]);

const schema = computed(() => {
  const validationsGroup = {};
  fields.value.forEach((field) => {
    let validations = yup;
    if (field.type === "number") validations = validations.number();
    if (["email", "text"].includes(field.type))
      validations = validations.string();

    if (field.required) validations = validations = validations.required();
    if (field.type === "email") validations = validations.email();

    validationsGroup[field.key] = validations.label(field.title);
  });
  return validationsGroup;
});

function onSubmit(values) {
  console.log(values, null, 2);
}
</script>
<template>
  <div class="card">
    <h4>Dynamic Field Example</h4>
    <hr />

    <Form @submit="onSubmit" :validation-schema="schema">
      <div v-for="{ key, title, type } in fields" :key="key" class="form-group">
        <label :for="key">{{ title }}</label>
        <Field :id="key" :name="key" :type="type" />
        <ErrorMessage :name="key" class="error-text" />
      </div>

      <button>Save</button>
    </Form>
  </div>
</template>
