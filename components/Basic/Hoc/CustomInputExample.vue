<script setup>
import { Form, Field, ErrorMessage } from "vee-validate";

const GENDER = ["Male", "Female"];

function onSubmit(values) {
  console.log(values, null, 2);
}

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

function validateRequired(value) {
  // if the field is empty
  if (!value) {
    return "This field is required";
  }
  // All is good
  return true;
}

function validatePassword(value) {
  // if the field is empty
  if (!value) {
    return "This field is required";
  }
  // All is good
  return true;
}
</script>

<template>
  <div class="card">
    <h4>Custom Component Field Example</h4>
    <hr />

    <Form @submit="onSubmit" v-slot="{ errors }">
      <div class="form-group">
        <label for="email">Email</label>
        <Field
          name="email"
          type="email"
          :rules="validateEmail"
          :class="{
            'error-field': !!errors.email,
          }"
        />
        <ErrorMessage name="email" class="error-text" />
      </div>

      <div class="form-group">
        <label for="password">Password</label>
        <Field
          name="password"
          type="password"
          :rules="validatePassword"
          validateOnInput
          :class="{
            'error-field': !!errors.password,
          }"
        />
        <ErrorMessage name="password" class="error-text" />
      </div>

      <div class="form-group">
        <label for="gender">Gender</label>
        <Field
          v-slot="{ value }"
          name="gender"
          as="select"
          :rules="validateRequired"
          :class="{
            'error-field': !!errors.gender,
          }"
        >
          <option value="" disabled>Select Gender</option>
          <option
            v-for="item in GENDER"
            :key="item"
            :value="item"
            :selected="value && value.includes(item)"
          >
            {{ item }}
          </option>
        </Field>
        <ErrorMessage name="gender" class="error-text" />
      </div>

      <button>Sign In</button>
    </Form>
  </div>
</template>
