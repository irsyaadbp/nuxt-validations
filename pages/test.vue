<template>
  <div class="container">
    <form @submit.prevent="handleSubmit">
      <base-input
        v-model="$v.firstName.$model"
        :error-messages="$v.firstName.$errors"
      />
      <base-input
        v-model="form.lastName"
        :error-messages="$v.lastName.$errors?.[0]?.$message"
      />
      <base-input
        v-model="form.contact.email"
        :error-messages="$v.contact.email.$errors?.[0]?.$message"
      />
      <button>Submit</button>
    </form>
  </div>
</template>

<script setup lang="ts">
import useVuelidate from "@vuelidate/core";
import { required, minLength, email, helpers } from "@vuelidate/validators";

const form = ref({
  firstName: "",
  lastName: "",
  contact: {
    email: "",
  },
});

const rules = {
  firstName: {
    required: helpers.withMessage("This field wajib", required),
    minLength: minLength(4),
  },
  lastName: { required },
  contact: {
    email: { email },
  },
};

const $v = useVuelidate(rules, form, { $autoDirty: true });

async function handleSubmit() {
  const valid = await $v.value.$validate();
  console.log(valid);

  if (!valid) return;

  alert("SUBMIT FORM");
}
</script>

<style scoped></style>
