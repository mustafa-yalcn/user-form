<template>
  <div class="relative bg-white rounded-xl shadow-xl p-6 pt-16 w-full max-w-md">
    <h2 class="text-xl font-semibold text-center text-gray-800 mb-6">Kullanıcı Bilgileri</h2>
    <p v-if="errorMessage" class="text-sm text-red-600 text-center mb-4">{{ errorMessage }}</p>
    <p v-if="successMessage" class="text-sm text-green-600 text-center mb-4">{{ successMessage }}</p>

    <form @submit.prevent="handleSubmit" class="space-y-4">
      <div>
        <label class="text-sm text-gray-600 mb-1 block">Ad</label>
        <input v-model="firstName" type="text" placeholder="Adınız"
          class="w-full border border-gray-300 rounded-md px-3 py-2 focus:outline-none focus:ring-2 focus:ring-indigo-500"/>
      </div>
      <div>
        <label class="text-sm text-gray-600 mb-1 block">Soyad</label>
        <input v-model="lastName" type="text" placeholder="Soyadınız"
          class="w-full border border-gray-300 rounded-md px-3 py-2 focus:outline-none focus:ring-2 focus:ring-indigo-500"/>
      </div>
      <div>
        <label class="text-sm text-gray-600 mb-1 block">E-posta</label>
        <input v-model="email" type="email" placeholder="E-posta adresiniz"
          class="w-full border border-gray-300 rounded-md px-3 py-2 focus:outline-none focus:ring-2 focus:ring-indigo-500"/>
      </div>

      <button type="submit"
        class="w-full mt-4 bg-indigo-600 text-white font-semibold py-2 rounded-md hover:bg-indigo-700 transition-colors">
        Kaydet
      </button>
    </form>
  </div>
</template>

<script setup>
import { defineModel, ref, defineEmits } from 'vue'

const firstName = defineModel('firstName')
const lastName = defineModel('lastName')
const email = defineModel('email')
const emit = defineEmits(['success'])

const errorMessage = ref('')
const successMessage = ref('')

async function handleSubmit() {
  errorMessage.value = ''
  successMessage.value = ''

  if (!firstName.value || !lastName.value || !email.value) {
    errorMessage.value = 'Lütfen tüm alanları doldurun.'
    return
  }

  try {
    const response = await fetch('https://jsonplaceholder.typicode.com/posts', {
      method: 'POST',
      headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify({
        firstName: firstName.value,
        lastName: lastName.value,
        email: email.value
      })
    })

    if (!response.ok) throw new Error('Gönderim başarısız.')

    successMessage.value = '✅ Bilgiler başarıyla kaydedildi!'
    setTimeout(() => {
      successMessage.value = ''
      emit('success')
    }, 1500)

  } catch (err) {
    errorMessage.value = 'Bir hata oluştu. Lütfen tekrar deneyin.'
    console.error(err)
  }
}
</script>
