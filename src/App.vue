<template>
  <Suspense>
    <template #default>
      <AppContent />
    </template>
    <template #fallback>
      <p>Yükleniyor...</p>
    </template>
  </Suspense>
</template>

<script setup>
import AppContent from './components/FormContent.vue'
</script>
