<script setup>
import { useForm } from "vee-validate";

function validateEmail(value) {
  // if the field is empty
  if (!value) {
    return "This field is required";
  }
  // if the field is not a valid email
  const regex = /^[A-Z0-9._%+-]+@[A-Z0-9.-]+\.[A-Z]{2,4}$/i;
  if (!regex.test(value)) {
    return "This field must be a valid email";
  }
  // All is good
  return true;
}

function validatePassword(value) {
  if (!value) {
    return "this field is required";
  }

  return true;
}
const simpleSchema = {
  email: validateEmail,
  password: validatePassword,
};

const { handleSubmit, handleReset } = useForm({
  validationSchema: simpleSchema,
});

const submit = handleSubmit((values) => {
  console.log({ values });
  alert("Submit Form");
});
</script>

<template>
  <div class="card">
    <h4>Form Level Validation Example</h4>
    <hr />
    <form @submit.prevent="submit">
      <label for="email">Email</label>
      <BasicCompositionInputForm name="email" />

      <label for="password">Password</label>
      <BasicCompositionInputForm name="password" />

      <button type="button" @click="handleReset">Reset</button>
      <button type="submit">Submit</button>
    </form>
  </div>
</template>
