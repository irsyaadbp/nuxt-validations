<script setup>
import { ErrorMessage, Field, Form } from "vee-validate";

import * as yup from "yup";

const schema = yup.object({
  user: yup.object({
    email: yup.string().required().email().label("Email"),
    password: yup.string().required().min(8).label("Password"),
  }),
});

const onSubmit = (values) => {
  console.log({ values });
  alert("SUBMIT FORM");
};
</script>
<template>
  <div class="card">
    <h4>Nested Object Example</h4>
    <hr />

    <Form @submit="onSubmit" :validation-schema="schema">
      <div class="form-group">
        <label for="user.email">Email</label>
        <Field name="user.email" type="email" validateOnInput />
        <ErrorMessage name="user.email" class="error-text" />
      </div>

      <div class="form-group">
        <label for="user.password">Password</label>
        <Field name="user.password" type="password" validateOnInput />
        <ErrorMessage name="user.password" class="error-text" />
      </div>
      <button>Sign In</button>
    </Form>
  </div>
</template>
