<script setup>
import { ErrorMessage, Field, Form } from "vee-validate";
import * as yup from "yup";

const schema = yup.object({
  email: yup.string().required().email(),
  password: yup.string().required().min(8),
});

const onSubmit = (values) => {
  console.log({ values });
  alert("SUBMIT FORM");
};
</script>
<template>
  <div class="card">
    <h4>Simple Yup Example</h4>
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
