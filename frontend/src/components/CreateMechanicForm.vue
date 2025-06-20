<template>
  <div class="create-mechanic">
    <h3>Create Mechanic</h3>
    <button @click="createMechanic">Create for Workshop</button>
  </div>
</template>

<script setup>
import axios from 'axios';
import { defineProps, watch } from 'vue';

const props = defineProps({
  workshopId: String
});

watch(() => props.workshopId, val => { /* no-op - to track reactivity */ });

async function createMechanic() {
  if (!props.workshopId) return;
  await axios.post('/mechanics', { workshopId: props.workshopId });
  emit('created');
}

const emit = defineEmits(['created']);
</script>

<style scoped>
.create-mechanic {
  margin: 20px 0;
}
</style>
