<template>
  <div class="w-full max-w-6xl mx-auto flex flex-col md:flex-row bg-gray-100 rounded-2xl shadow-lg overflow-hidden mt-12">
    <div class="md:w-1/2 bg-gradient-to-br from-indigo-500 to-purple-600 flex flex-col items-center justify-center text-white p-10">
      <h2 class="text-3xl font-bold text-center">HOŞGELDİNİZ!</h2>
      <p class="text-center mt-4 max-w-sm">Modern bir profil formu.</p>
    </div>
    <div class="md:w-1/2 flex items-center justify-center p-6">
      <UserForm
        v-model:firstName="firstName"
        v-model:lastName="lastName"
        v-model:email="email"
        @success="onSuccess"
      />
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import UserForm from './UserForm.vue'

const firstName = ref('')
const lastName = ref('')
const email = ref('')

function onSuccess() {
  firstName.value = ''
  lastName.value = ''
  email.value = ''
}
</script>
