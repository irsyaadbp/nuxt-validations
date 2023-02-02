<script setup>
import { Form, Field, ErrorMessage } from "vee-validate";

function onSubmit(values) {
  console.log(values, null, 2);
}

const simpleSchema = {
  email(value) {
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
  },
  password(value) {
    // if the field is empty
    if (!value) {
      return "This field is required";
    }
    // All is good
    return true;
  },
};
</script>

<template>
  <div class="card">
    <h4>Form Level Validation Example</h4>
    <hr />

    <Form @submit="onSubmit" :validationSchema="simpleSchema">
      <div class="form-group">
        <label for="email">Email</label>
        <Field name="email" type="email" />
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
