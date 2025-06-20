<template>
  <div>
    <h4>Create Skill Area</h4>
    <input v-model="area" placeholder="Area" />
    <select v-model="level">
      <option>JUNIOR</option>
      <option>MID</option>
      <option>SENIOR</option>
    </select>
    <button @click="create">Add</button>
  </div>
</template>

<script setup>
import { ref } from 'vue';
import axios from 'axios';

const props = defineProps({ mechanicId: String });
const emit = defineEmits(['created']);

const area = ref('');
const level = ref('JUNIOR');

async function create() {
  await axios.post(`/mechanics/${props.mechanicId}/skill-areas`, {
    area: area.value,
    level: level.value
  });
  area.value = '';
  emit('created');
}
</script>
