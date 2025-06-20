<template>
  <div>
    <h4>Create Work Day</h4>
    <label>Day:</label>
    <select v-model="day">
      <option>MONDAY</option>
      <option>TUESDAY</option>
      <option>WEDNESDAY</option>
      <option>THURSDAY</option>
      <option>FRIDAY</option>
      <option>SATURDAY</option>
      <option>SUNDAY</option>
    </select>
    <label>Start:</label>
    <input type="time" v-model="start" />
    <label>End:</label>
    <input type="time" v-model="end" />
    <button @click="create">Add</button>
  </div>
</template>

<script setup>
import { ref } from 'vue';
import axios from 'axios';

const props = defineProps({ mechanicId: String });
const emit = defineEmits(['created']);

const day = ref('MONDAY');
const start = ref('09:00');
const end = ref('17:00');

async function create() {
  await axios.post(`/mechanics/${props.mechanicId}/work-days`, {
    day: day.value,
    startAt: start.value,
    endAt: end.value
  });
  emit('created');
}
</script>

<style scoped>
label {
  margin-right: 5px;
}
</style>
