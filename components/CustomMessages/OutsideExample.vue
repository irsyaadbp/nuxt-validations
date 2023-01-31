<script setup>
import { reactive } from "vue";
import { useVuelidate } from "@vuelidate/core";
import { required, minLength, email, helpers } from "@vuelidate/validators";

const form = reactive({
  firstName: "",
  lastName: "",
  contact: {
    email: "",
  },
});

const $externalResults = ref({}); // works with reactive({}) too.
const loading = ref(false);

const rules = {
  firstName: {
    required: helpers.withMessage("This field must be filled", required),
    minLength: helpers.withMessage(
      ({ $pending: _$pending, $invalid, $params, $model }) =>
        `This field has a value of '${$model}' but must have a min length of ${
          $params.min
        } so it is ${$invalid ? "invalid" : "valid"}`,
      minLength(4)
    ),
  },
  lastName: { required },
  contact: { email: { required, email } },
};

const v$ = useVuelidate(rules, form, { $autoDirty: true, $externalResults });

/**
 * Function to mock API from server with response error
 */
function saveToServer() {
  return new Promise((_resolve, reject) => {
    const timeout = setTimeout(() => {
      reject({
        error: {
          firstName: ["First name must be unique", "First name is too long"],
        },
      });
      clearTimeout(timeout);
    }, 1000);
  });
}

/**
 * Function to submit form
 */
async function handleSubmit() {
  try {
    const isValidForm = await v$.value.$validate();

    if (!isValidForm) {
      console.log("invalid");
      return;
    }

    loading.value = true;

    await saveToServer();

    alert("SUBMIT FORM");
  } catch (error) {
    $externalResults.value = error?.error;
  } finally {
    loading.value = false;
  }
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
    <h4>Outside Example</h4>
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
      <button @click="handleReset" :disabled="loading">Reset</button>
      <button @click="handleSubmit" :disabled="loading">
        {{ loading ? "Loading..." : "Save" }}
      </button>
    </div>
  </div>
</template>
