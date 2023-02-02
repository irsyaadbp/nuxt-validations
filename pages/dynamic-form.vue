<template>
  <div class="container">
    <div class="d-flex gap-8 align-items-center">
      <NuxtLink to="/"> &#8592; </NuxtLink>
      <h2>Dynamic Form</h2>
    </div>

    <collapse-item>
      <template #title> HOC </template>
      <template #default>
        <DynamicHocArrayExample />
        <DynamicHocFieldExample />
      </template>
    </collapse-item>

    <collapse-item>
      <template #title> Composition </template>
      <template #default>
        <DynamicCompositionArrayExample />
        <DynamicCompositionFieldExample />
      </template>
    </collapse-item>
  </div>
</template>
