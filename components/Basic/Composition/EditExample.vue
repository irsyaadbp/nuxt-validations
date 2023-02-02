<script setup>
import { useForm } from "vee-validate";

const users = ref([
  { id: 1, email: "email@mail.com", name: "John Doe" },
  { id: 2, email: "budi@mail.com", name: "Budi Sudarsono" },
]);

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
  if (!value) {
    return "this field is required";
  }

  return true;
}
const simpleSchema = {
  email: validateEmail,
  name: validateName,
};

const { handleSubmit, handleReset, setValues, errors } = useForm({
  validationSchema: simpleSchema,
});

const submit = handleSubmit((values) => {
  users.value = users.value.map((user) => {
    if (user.id === values.id) {
      return values;
    }
    return user;
  });
  handleReset();
});

function handleEdit(user) {
  setValues(user);
}
</script>

<template>
  <div class="card">
    <h4>Edit Set Value Example</h4>
    <hr />
    <form @submit.prevent="submit">
      <label for="email">Email</label>
      <BasicCompositionInputForm name="email" />

      <label for="name">Name</label>
      <BasicCompositionInputForm name="name" />

      <button type="button" @click="handleReset">Reset</button>
      <button type="submit">Submit</button>
    </form>

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
