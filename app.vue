<template>
  <NuxtPage />
</template>

<style lang="css">
body {
  font-family: "Gill Sans", "Gill Sans MT", Calibri, "Trebuchet MS", sans-serif;
}

.d-flex {
  display: flex;
}

.justify-content-center {
  justify-content: center;
}
.justify-content-start {
  justify-content: flex-start;
}
.justify-content-end {
  justify-content: flex-end;
}

.align-items-center {
  align-items: center;
}

.align-items-start {
  align-items: start;
}

.align-items-end {
  align-items: end;
}

label {
  display: block;
}

.container {
  max-width: 100%;
  margin: 0 auto;
}

.card {
  padding: 8px;
  border: thin solid;
  border-radius: 4px;

  margin-bottom: 12px;
}

input {
  padding: 4px;
  border-radius: 4px;
}

input.error-field {
  border-color: red;
}

.error-text {
  color: red;
}

.form-group {
  margin-bottom: 10px;
  display: flex;
  flex-direction: column;
}

.gap-8 {
  gap: 8px;
}

.gap-16 {
  gap: 16px;
}

p {
  margin: 0;
}

a {
  text-decoration: none;
  color: blue;
}

li {
  font-size: 20px;
  margin-bottom: 10px;
}

@media only screen and (min-width: 992px) {
  .container {
    max-width: 30vw;
  }
}
</style>
