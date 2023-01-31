<script setup>
import { reactive } from "vue";
import { useVuelidate } from "@vuelidate/core";
import { required, email, helpers } from "@vuelidate/validators";

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
// check the email in the serverƒ

const isUniqueEmail = helpers.withAsync(checkToServerEmailUnique);

const form = reactive({
  firstName: "",
  lastName: "",
  contact: {
    email: "",
  },
});

const rules = {
  firstName: {
    required,
  },
  lastName: {
    required,
  },
  contact: {
    email: {
      required,
      email,

      isUnique: helpers.withMessage(
        ({ $model }) => `This email '${$model}' has been taken`,
        isUniqueEmail
      ),
    },
  },
};

const v$ = useVuelidate(rules, form, { $autoDirty: true });

/**
 * Function to submit form
 */
async function handleSubmit() {
  const isValidForm = await v$.value.$validate();

  if (!isValidForm) {
    console.log("invalid");
    return;
  }

  alert("SUBMIT FORM");
}

/**
 * Function to reset vuelidate
 */
function handleReset() {
  v$.value.$reset();
}
</script>

<template>
  <div class="card">
    <h4>Asynchronouse Validations Example</h4>
    <hr />
    <div class="form-group">
      <label for="fullName">Full Name</label>
      <input
        type="text"
        v-model="form.firstName"
        :class="{ 'error-field': v$.firstName.$invalid && v$.firstName.$dirty }"
      />

      <p
        v-for="error of v$.firstName.$errors"
        :key="error.$uid"
        class="error-text"
      >
        <small>{{ error.$message }}</small>
      </p>
    </div>

    <div class="form-group">
      <label for="lastName">Last Name</label>
      <input
        type="text"
        v-model="form.lastName"
        :class="{ 'error-field': v$.lastName.$invalid && v$.lastName.$dirty }"
      />

      <p
        v-for="error of v$.lastName.$errors"
        :key="error.$uid"
        class="error-text"
      >
        <small>{{ error.$message }}</small>
      </p>
    </div>

    <div class="form-group">
      <label for="email">Email</label>
      <input
        type="text"
        v-model="form.contact.email"
        :class="{
          'error-field': v$.contact.email.$invalid && v$.contact.email.$dirty,
        }"
      />

      <p
        v-for="error of v$.contact.email.$errors"
        :key="error.$uid"
        class="error-text"
      >
        <small>{{ error.$message }}</small>
      </p>
    </div>

    <div class="d-flex justify-content-end gap-8">
      <button @click="handleReset">Reset</button>
      <button @click="handleSubmit">Save</button>
    </div>
  </div>
</template>
