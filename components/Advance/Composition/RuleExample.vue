<script setup>
import { defineRule, useForm } from "vee-validate";
import { required } from "@vee-validate/rules";

defineRule("required", required);

const checkToServerEmailUnique = (value) =>
  new Promise((resolve) => {
    const timeout = setTimeout(() => {
      clearTimeout(timeout);
      if (value === "email@mail.com") {
        resolve(false); // open this to try when error
        return;
      }
      resolve(true); // open this to try when success
    }, 500);
  });

async function validateEmail(value) {
  // if the field is empty
  if (!value) {
    return "This field is required";
  }
  // if the field is not a valid email
  const regex = /^[A-Z0-9._%+-]+@[A-Z0-9.-]+\.[A-Z]{2,4}$/i;
  if (!regex.test(value)) {
    return "This field must be a valid email";
  }

  const isUnique = await checkToServerEmailUnique(value);

  if (!isUnique) {
    return `This email '${value}' has been taken`;
  }
  // All is good
  return true;
}

defineRule("minLength", (value, [limit]) => {
  // The field is empty so it should pass
  if (!value || !value.length) {
    return true;
  }
  if (value.length < limit) {
    return `This field must be at least ${limit} characters`;
  }
  return true;
});

const schema = {
  email: validateEmail,
  password: "required|minLength:8",
};

const { handleReset, handleSubmit } = useForm({
  validationSchema: schema,
});

const submit = handleSubmit((values) => {
  console.log({ values });
  alert("Submit Form");
});
</script>
<template>
  <div class="card">
    <h4>Simple Rule Example</h4>
    <hr />

    <form @submit.prevent="submit">
      <label for="email">Email</label>
      <AdvanceCompositionInputForm name="email" />

      <label for="password">Password</label>
      <AdvanceCompositionInputForm name="password" />

      <button type="button" @click="handleReset">Reset</button>
      <button type="submit">Submit</button>
    </form>
  </div>
</template>
