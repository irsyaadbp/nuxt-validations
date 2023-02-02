<script setup>
import { Field, Form, ErrorMessage, FieldArray } from "vee-validate";
import * as yup from "yup";

const initialData = {
  users: [
    {
      name: "",
      email: "",
    },
  ],
};

const schema = yup.object().shape({
  users: yup
    .array()
    .of(
      yup.object().shape({
        name: yup.string().required().label("Name"),
        email: yup.string().email().required().label("Email"),
      })
    )
    .strict(),
});

function onSubmit(values) {
  console.log(JSON.stringify(values, null, 2));
}
</script>

<template>
  <div class="card">
    <h4>Array Example</h4>
    <hr />
    <Form
      @submit="onSubmit"
      :initial-values="initialData"
      :validation-schema="schema"
    >
      <p></p>

      <FieldArray name="users" v-slot="{ fields, push, remove }">
        <fieldset
          v-for="(field, idx) in fields"
          :key="field.key"
          style="margin-bottom: 4px"
        >
          <legend>User #{{ idx + 1 }}</legend>
          <div class="form-group">
            <label :for="`name_${idx}`">Name</label>
            <Field :id="`name_${idx}`" :name="`users[${idx}].name`" />
            <ErrorMessage :name="`users[${idx}].name`" class="error-text" />
          </div>

          <div class="form-group">
            <label :for="`email_${idx}`">Email</label>
            <Field
              :id="`email_${idx}`"
              :name="`users[${idx}].email`"
              type="email"
            />
            <ErrorMessage :name="`users[${idx}].email`" class="error-text" />
          </div>
          <button title="Delete User" type="button" @click="remove(idx)">
            X
          </button>
        </fieldset>

        <button type="button" @click="push({ email: '', name: '' })">
          Add User +
        </button>
      </FieldArray>

      <button type="submit">Submit</button>
    </Form>
  </div>
</template>
