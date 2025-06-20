<template>
  <div class="skill-certifications">
    <h4>Certifications</h4>
    <ul>
      <li v-for="c in certifications" :key="c.id">
        {{ c.certificationName }} - {{ c.issuer }}
      </li>
    </ul>
    <create-skill-certification-form
      :mechanic-id="mechanicId"
      :skill-area-id="skillAreaId"
      @created="load"
    />
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import axios from 'axios';
import CreateSkillCertificationForm from './CreateSkillCertificationForm.vue';

const props = defineProps({
  mechanicId: String,
  skillAreaId: String
});
const certifications = ref([]);

async function load() {
  const url = `/mechanics/${props.mechanicId}/skill-areas/${props.skillAreaId}/skill-certifications`;
  const response = await axios.get(url);
  certifications.value = response.data;
}

onMounted(load);
</script>

<style scoped>
.skill-certifications {
  margin-top: 10px;
  padding-left: 20px;
}
</style>
