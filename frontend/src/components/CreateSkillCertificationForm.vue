<template>
  <div>
    <h5>Add Certification</h5>
    <input v-model="certificationName" placeholder="Name" />
    <input v-model="issuer" placeholder="Issuer" />
    <input type="date" v-model="issueDate" />
    <input type="date" v-model="expirationDate" />
    <input type="file" @change="onFile" />
    <button @click="create">Upload</button>
  </div>
</template>

<script setup>
import { ref } from 'vue';
import axios from 'axios';

const props = defineProps({
  mechanicId: String,
  skillAreaId: String
});
const emit = defineEmits(['created']);

const certificationName = ref('');
const issuer = ref('');
const issueDate = ref('');
const expirationDate = ref('');
let file = null;

function onFile(e) {
  file = e.target.files[0];
}

async function create() {
  const form = new FormData();
  form.append('resource.certificationName', certificationName.value);
  form.append('resource.issuer', issuer.value);
  form.append('resource.issueDate', issueDate.value);
  form.append('resource.expirationDate', expirationDate.value);
  if (file) form.append('file', file);
  const url = `/mechanics/${props.mechanicId}/skill-areas/${props.skillAreaId}/skill-certifications`;
  await axios.post(url, form, {
    headers: { 'Content-Type': 'multipart/form-data' }
  });
  emit('created');
}
</script>
