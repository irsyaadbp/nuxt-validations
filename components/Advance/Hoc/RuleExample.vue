<script setup>
import { defineRule, ErrorMessage, Field, Form } from "vee-validate";
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

const onSubmit = (values) => {
  console.log({ values });
  alert("SUBMIT FORM");
};
</script>
<template>
  <div class="card">
    <h4>Simple Rule Example</h4>
    <hr />

    <Form @submit="onSubmit" :validation-schema="schema">
      <div class="form-group">
        <label for="email">Email</label>
        <Field name="email" type="email" validateOnInput />
        <ErrorMessage name="email" class="error-text" />
      </div>

      <div class="form-group">
        <label for="password">Password</label>
        <Field name="password" type="password" validateOnInput />
        <ErrorMessage name="password" class="error-text" />
      </div>
      <button>Sign In</button>
    </Form>
  </div>
</template>
