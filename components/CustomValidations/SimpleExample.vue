<script setup>
import { reactive } from "vue";
import { useVuelidate } from "@vuelidate/core";
import { required, minLength, email, helpers } from "@vuelidate/validators";

/**
 * Custom validations
 * this custom validation is required because if value empty it means not contain "cool"
 */
const mustBeCool = (value) => value.includes("cool");

/**
 * Custom validations not required
 */
const mustBeCoolNotRequired = (value) =>
  !helpers.req(value) || value.includes("cool");

/**
 * Custom validations with regex
 */
const alpha = helpers.regex(/^[a-zA-Z]*$/);

const form = reactive({
  firstName: "",
  lastName: "",
  contact: {
    email: "",
  },
});

const rules = {
  firstName: {
    minLength: minLength(3),
    mustBeCool: helpers.withMessage(
      "Value cant empty and must be contain cool",
      mustBeCool
    ),
  },
  lastName: {
    mustBeCool: helpers.withMessage(
      "Value must be contain cool",
      mustBeCoolNotRequired
    ),
    alpha: helpers.withMessage("Value must be alphabet only", alpha),
  },
  contact: { email: { required, email } },
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
    <h4>Simple Example</h4>
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
