<script setup>
import { Form, Field, ErrorMessage } from "vee-validate";

const users = ref([
  { id: 1, email: "email@mail.com", name: "John Doe" },
  { id: 2, email: "budi@mail.com", name: "Budi Sudarsono" },
]);
const myForm = ref(null);

function onSubmit(values) {
  users.value = users.value.map((user) => {
    if (user.id === values.id) {
      return values;
    }
    return user;
  });
  handleReset();
}
function handleEdit(user) {
  myForm.value.setValues(user);
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

function validateName(value) {
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
    <h4>Edit Set Value Example</h4>
    <hr />

    <Form ref="myForm" @submit="onSubmit">
      <div class="form-group">
        <label for="email">Email</label>
        <Field name="email" type="email" :rules="validateEmail" />
        <ErrorMessage name="email" class="error-text" />
      </div>

      <div class="form-group">
        <label for="name">Full Name</label>
        <Field name="name" type="name" :rules="validateName" validateOnInput />
        <ErrorMessage name="name" class="error-text" />
      </div>
      <button>Save</button>
    </Form>

    <hr />
    <table>
      <thead>
        <tr>
          <th>No.</th>
          <th>Email</th>
          <th>Fullname</th>
          <th>Action</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="user in users" :key="`user-${user.id}`">
          <td>{{ user.id }}.</td>
          <td>{{ user.email }}</td>
          <td>{{ user.name }}</td>
          <td><button @click="handleEdit(user)">Edit</button></td>
        </tr>
      </tbody>
    </table>
  </div>
</template>
