<template>
  <div>
    <fieldset
      v-for="(f, index) in form"
      :key="`form-${index}`"
      style="margin-bottom: 1rem"
    >
      <SectionForm :form="f" />
    </fieldset>
  </div>
</template>

<script setup lang="ts">
const api = {
  status: "SUCCESS",
  entity: "getFormStructureV2",
  state: "getFormStructureV2Success",
  message: "OK",
  data: {
    application_id: "d08efc22-d0fa-4505-bbd3-c0c3a200e115",
    forms: {
      form_setup: {
        id: "0142a196-3372-41b5-b9e1-029c7a827680",
        application_id: "d08efc22-d0fa-4505-bbd3-c0c3a200e115",
        form: [
          {
            sequence: 1,
            data_type: "personal_information_1",
            component_type: "section",
            label: {
              en: "Personal Information 1",
              id: "Informasi Personal 1",
            },
            description: {
              en: "this is 1st section",
              id: "ini adalah section 1",
            },
            element: [
              {
                sequence: 1,
                component_type: "file",
                data_type: "resume",
                label: {
                  en: "Resume",
                  id: "Resume",
                },
                description: {
                  en: "Resume",
                  id: "Resumeid",
                },
                placeholder: {
                  en: "Upload",
                  id: "Unggah",
                },
                rules: {
                  required: true,
                  reusable: false,
                  verified: false,
                },
                permissions: [
                  {
                    access: ["read", "write"],
                    provider: "user",
                  },
                  {
                    access: ["read"],
                    provider: "merchant",
                  },
                ],
              },
              {
                sequence: 2,
                component_type: "short_text",
                data_type: "member1_fullname",
                label: {
                  en: "Full name",
                  id: "Nama lengkap",
                },
                description: {
                  en: "Full name",
                  id: "Nama lengkap",
                },
                placeholder: {
                  en: "Enter Full name",
                  id: "Masukkan Nama lengkap",
                },
                rules: {
                  required: false,
                  reusable: false,
                  verified: false,
                },
                permissions: [
                  {
                    access: ["read", "write"],
                    provider: "user",
                  },
                  {
                    access: ["read"],
                    provider: "merchant",
                  },
                ],
              },
              {
                sequence: 3,
                component_type: "image",
                data_type: "birth_certificate",
                label: {
                  en: "Birth certificate",
                  id: "Akta kelahiran",
                },
                description: {
                  en: "Birth Certificate",
                  id: "Akta Kelahiran",
                },
                placeholder: {
                  en: "Upload",
                  id: "Unggah",
                },
                rules: {
                  required: false,
                  reusable: false,
                  verified: false,
                },
                permissions: [
                  {
                    access: ["read", "write"],
                    provider: "user",
                  },
                  {
                    access: ["read"],
                    provider: "merchant",
                  },
                ],
              },
            ],
          },
          {
            sequence: 2,
            data_type: "personal_information_2",
            component_type: "section",
            label: {
              en: "Personal Information 2",
              id: "Informasi Personal 2",
            },
            description: {
              en: "this is 2nd section",
              id: "ini adalah section 2",
            },
            element: [
              {
                sequence: 1,
                component_type: "short_text",
                data_type: "job_company_name",
                label: {
                  en: "Company name",
                  id: "Nama perusahaan",
                },
                description: {
                  en: "Compan yname",
                  id: "Nama perusahaan",
                },
                placeholder: {
                  en: "PT Privy Identitas Digital",
                  id: "PT Privy Identitas Digital",
                },
                rules: {
                  required: false,
                  reusable: false,
                  verified: false,
                },
                permissions: [
                  {
                    access: ["read", "write"],
                    provider: "user",
                  },
                  {
                    access: ["read"],
                    provider: "merchant",
                  },
                ],
              },
              {
                sequence: 2,
                component_type: "image",
                data_type: "income_pay_slip",
                label: {
                  en: "Pay slip",
                  id: "Slip gaji",
                },
                description: {
                  en: "Pay slip",
                  id: "Slip gaji",
                },
                placeholder: {
                  en: "Upload",
                  id: "Unggah",
                },
                rules: {
                  required: false,
                  reusable: false,
                  verified: false,
                },
                permissions: [
                  {
                    access: ["read", "write"],
                    provider: "user",
                  },
                  {
                    access: ["read"],
                    provider: "merchant",
                  },
                ],
              },
            ],
          },
        ],
        is_active: true,
        created_at: "2023-05-24T10:56:09.191009+07:00",
        updated_at: "2023-06-12T06:50:39.305565+07:00",
      },
    },
  },
};

const form = ref<any[]>([]);

function getData() {
  return new Promise<any>((resolve) => {
    const timeout = setTimeout(() => {
      resolve(api);
      clearTimeout(timeout);
    }, 1000);
  });
}

onMounted(() => {
  getData().then((data) => {
    form.value = data?.data?.forms?.form_setup?.form;
  });
});
</script>

<style scoped></style>
