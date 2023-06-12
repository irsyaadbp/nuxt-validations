<template>
  <Form :validation-schema="schema" @submit="handleSubmit">
    <div class="form-group">
      <base-input
        v-for="element in form?.element"
        :name="element.data_type"
        :type="element.component_type"
      />
    </div>

    <button>Submit</button>
  </Form>
</template>

<script setup lang="ts">
import { Form } from "vee-validate";
import * as yup from "yup";

const props = defineProps({
  form: {
    type: Object,
    default: undefined,
  },
});

const { form } = toRefs(props);

const schema = computed(() => {
  const validationsGroup: Record<string, any> = {};
  (form?.value?.element || [])?.forEach((element: any) => {
    if (["text", "short_text"].includes(element.component_type))
      validationsGroup[element.data_type] = yup.string();
    if (["file"].includes(element.component_type))
      validationsGroup[element.data_type] = yup.mixed();

    if (element.rules.required)
      validationsGroup[element.data_type] =
        validationsGroup[element.data_type]?.required();

    if (element.label)
      validationsGroup[element.data_type] = validationsGroup[
        element.data_type
      ]?.label(element.label.id);
  });
  return validationsGroup;
});

function handleSubmit(values: any) {
  console.log(values);
}
</script>

<style scoped></style>
