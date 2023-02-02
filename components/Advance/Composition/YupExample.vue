<script setup>
import { useForm } from "vee-validate";
import * as yup from "yup";

const schema = yup.object({
  email: yup.string().required().email(),
  password: yup.string().required().min(8),
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
    <h4>Simple Yup Example</h4>
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
