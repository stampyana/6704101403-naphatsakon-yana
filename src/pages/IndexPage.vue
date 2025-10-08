<template>
  <q-page class="q-pa-md">
    <div class="q-gutter-md" style="max-width: 400px; margin: auto;">
      <q-form @submit="onSubmit" @reset="onReset" class="q-gutter-md">

        <q-input
          filled
          v-model="name"
          label="Your name"
          hint="Name and surname"
          lazy-rules
          :rules="[val => val && val.length > 0 || 'Please type something']"
        />

        <q-input
          filled
          type="number"
          v-model="age"
          label="Your age"
          lazy-rules
          :rules="[
            val => val !== null && val !== '' || 'Please type your age',
            val => val > 0 && val < 100 || 'Please type a real age'
          ]"
        />

        <q-toggle v-model="accept" label="I accept the license and terms" />

        <div class="row justify-around q-mt-md">
          <q-btn label="Submit" type="submit" color="primary" />
          <q-btn label="Reset" type="reset" color="secondary" flat />
        </div>

      </q-form>
    </div>
  </q-page>
</template>

<script setup>
import { ref } from 'vue'

const name = ref(null)
const age = ref(null)
const accept = ref(false)

function onSubmit () {
  if (accept.value !== true) {
    alert('You need to accept the license and terms first!')
    return
  }
  alert(`Submitted:\nName: ${name.value}\nAge: ${age.value}`)
}

function onReset () {
  name.value = null
  age.value = null
  accept.value = false
}
</script>
