<script setup>
import { useForm } from "vee-validate";
import * as yup from "yup";

const schema = yup.object({
  user: yup.object({
    email: yup.string().required().email().label("Email"),
    password: yup.string().required().min(8).label("Password"),
  }),
});

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
    <h4>Nested Object Example</h4>
    <hr />

    <form @submit.prevent="submit">
      <label for="user.email">Email</label>
      <AdvanceCompositionInputForm name="user.email" />

      <label for="user.password">Password</label>
      <AdvanceCompositionInputForm name="user.password" />

      <button type="button" @click="handleReset">Reset</button>
      <button type="submit">Submit</button>
    </form>
  </div>
</template>
