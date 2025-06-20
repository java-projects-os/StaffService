<template>
  <div class="skill-areas">
    <h3>Skill Areas</h3>
    <ul>
      <li v-for="s in skillAreas" :key="s.id">
        {{ s.area }} - {{ s.level }}
        <skill-certification-section
          :mechanic-id="mechanicId"
          :skill-area-id="s.id"
        />
      </li>
    </ul>
    <create-skill-area-form :mechanic-id="mechanicId" @created="load" />
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import axios from 'axios';
import CreateSkillAreaForm from './CreateSkillAreaForm.vue';
import SkillCertificationSection from './SkillCertificationSection.vue';

const props = defineProps({ mechanicId: String });
const skillAreas = ref([]);

async function load() {
  const response = await axios.get(`/mechanics/${props.mechanicId}/skill-areas`);
  skillAreas.value = response.data;
}

onMounted(load);
</script>

<style scoped>
.skill-areas {
  margin-top: 20px;
}
</style>
