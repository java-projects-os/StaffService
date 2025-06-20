<template>
  <div class="container">
    <h1>Staff Management</h1>
    <div class="workshop-form">
      <label>Workshop ID:</label>
      <input v-model="workshopId" placeholder="Enter workshop id" />
      <button @click="loadMechanics">Load Mechanics</button>
    </div>
    <create-mechanic-form :workshop-id="workshopId" @created="loadMechanics" />
    <mechanic-list
      :mechanics="mechanics"
      @select="selectMechanic"
    />
    <div v-if="selectedMechanic" class="details">
      <h2>Mechanic Details</h2>
      <mechanic-detail :mechanic="selectedMechanic" />
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';
import axios from 'axios';
import MechanicList from './components/MechanicList.vue';
import CreateMechanicForm from './components/CreateMechanicForm.vue';
import MechanicDetail from './components/MechanicDetail.vue';

const workshopId = ref('');
const mechanics = ref([]);
const selectedMechanic = ref(null);

async function loadMechanics() {
  if (!workshopId.value) return;
  const response = await axios.get(`/mechanics`, {
    params: { workshopId: workshopId.value }
  });
  mechanics.value = response.data;
}

function selectMechanic(mechanic) {
  selectedMechanic.value = mechanic;
}
</script>

<style scoped>
.container {
  font-family: Arial, Helvetica, sans-serif;
  padding: 20px;
}
.workshop-form {
  margin-bottom: 20px;
}
.details {
  margin-top: 40px;
  border-top: 1px solid #ccc;
  padding-top: 20px;
}
</style>
