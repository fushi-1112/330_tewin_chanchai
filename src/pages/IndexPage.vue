<template>
  <q-page class="q-pa-md">
    <q-card class="q-pa-lg" style="max-width:640px; margin:auto">
      <q-card-section>
        <div class="text-h6">Student Basic Form</div>
        <div class="text-subtitle2">Please fill in your details</div>
      </q-card-section>

      <q-card-section>
        <q-form @submit.prevent="onSubmit" ref="formRef">
          <q-input v-model="form.studentId" label="Student ID" outlined lazy-rules :rules="[val => !!val || 'Required']" />
          <q-input v-model="form.firstName" label="First name" outlined class="q-mt-sm" :rules="[val => !!val || 'Required']" />
          <q-input v-model="form.lastName" label="Last name" outlined class="q-mt-sm" :rules="[val => !!val || 'Required']" />
          <q-input v-model="form.email" label="Email" type="email" outlined class="q-mt-sm" :rules="[val => /.+@.+\..+/.test(val) || 'Invalid email']" />
          <div class="row q-mt-md">
            <q-btn label="Submit" color="primary" type="submit" />
            <q-btn label="Reset" flat class="q-ml-sm" @click="onReset" />
          </div>
        </q-form>
      </q-card-section>

      <q-card-section v-if="submitted">
        <div class="text-subtitle2">Submitted data</div>
        <pre>{{ form }}</pre>
      </q-card-section>
    </q-card>
  </q-page>
</template>

<script setup>
import { ref, reactive } from 'vue'

const form = reactive({
  studentId: '',
  firstName: '',
  lastName: '',
  email: ''
})
const submitted = ref(false)
const formRef = ref(null)

function onSubmit() {
  submitted.value = true
  // สำหรับทดสอบ Playwright เราเก็บค่าไว้ใน localStorage ด้วย
  localStorage.setItem('studentForm', JSON.stringify(form))
}

function onReset() {
  form.studentId = ''
  form.firstName = ''
  form.lastName = ''
  form.email = ''
  submitted.value = false
}
</script>

<style scoped>
pre {
  background: #f5f5f7;
  padding: 0.5rem;
  border-radius: 6px;
}
</style>
