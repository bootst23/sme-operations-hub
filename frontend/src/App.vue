<script setup>
import { ref } from 'vue';
import { getHealthStatus } from './services/api';

const message = ref('Not tested yet');
const loading = ref(false);
const error = ref('');

async function testBackendConnection() {
  loading.value = true;
  error.value = '';

  try {
    const data = await getHealthStatus();
    message.value = data.message;
  } catch (err) {
    error.value = err.message;
  } finally {
    loading.value = false;
  }
}
</script>

<template>
  <main>
    <h1>SME Operations Hub</h1>
    <p>Frontend-backend connection test</p>

    <button @click="testBackendConnection" :disabled="loading">
      {{ loading ? 'Testing...' : 'Test Backend Connection' }}
    </button>

    <p>Message: {{ message }}</p>
    <p v-if="error">Error: {{ error }}</p>
  </main>
</template>