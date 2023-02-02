<template>
  <div class="container">
    <div class="d-flex gap-8 align-items-center">
      <NuxtLink to="/"> &#8592; </NuxtLink>
      <h2>Basic Validations</h2>
    </div>

    <collapse-item>
      <template #title> HOC </template>
      <template #default>
        <BasicHocSimpleExample />
        <BasicHocCustomInputExample />
        <BasicHocFormLevelExample />
        <BasicHocEditExample />
      </template>
    </collapse-item>

    <collapse-item>
      <template #title> Composition </template>
      <template #default>
        <BasicCompositionSimpleExample />
        <BasicCompositionFormLevelExample />
        <BasicCompositionEditExample />
      </template>
    </collapse-item>
  </div>
</template>
