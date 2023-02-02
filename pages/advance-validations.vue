<template>
  <div class="container">
    <div class="d-flex gap-8 align-items-center">
      <NuxtLink to="/"> &#8592; </NuxtLink>
      <h2>Advance Validations</h2>
    </div>

    <collapse-item>
      <template #title> HOC </template>
      <template #default>
        <AdvanceHocRuleExample />
        <AdvanceHocYupExample />
        <AdvanceHocNestedExample />
      </template>
    </collapse-item>

    <collapse-item>
      <template #title> Composition </template>
      <template #default>
        <AdvanceCompositionRuleExample />
        <AdvanceCompositionYupExample />
        <AdvanceCompositionNestedExample />
      </template>
    </collapse-item>
  </div>
</template>
