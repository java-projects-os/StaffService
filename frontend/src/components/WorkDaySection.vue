<template>
  <div class="work-days">
    <h3>Work Days</h3>
    <ul>
      <li v-for="w in workDays" :key="w.id">
        {{ w.day }}: {{ w.startAt }} - {{ w.endAt }}
      </li>
    </ul>
    <create-work-day-form :mechanic-id="mechanicId" @created="load" />
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import axios from 'axios';
import CreateWorkDayForm from './CreateWorkDayForm.vue';

const props = defineProps({ mechanicId: String });
const workDays = ref([]);

async function load() {
  const response = await axios.get(`/mechanics/${props.mechanicId}/work-days`);
  workDays.value = response.data;
}

onMounted(load);
</script>

<style scoped>
.work-days {
  margin-top: 20px;
}
</style>
