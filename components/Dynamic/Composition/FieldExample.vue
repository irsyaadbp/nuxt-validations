<script setup>
import { useForm } from "vee-validate";
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

const { handleSubmit } = useForm({
  validationSchema: schema,
});

const onSubmit = handleSubmit((values) => {
  console.log({ values });
  alert("Submit Form");
});
</script>

<template>
  <div class="card">
    <h4>Dynamic Field Example</h4>
    <hr />

    <form @submit="onSubmit">
      <div v-for="{ key, title, type } in fields" :key="key" class="form-group">
        <label :for="key">{{ title }}</label>
        <DynamicCompositionInputForm :name="key" :type="type" />
      </div>

      <button>Save</button>
    </form>
  </div>
</template>
