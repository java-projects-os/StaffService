<template>
  <div>
    <p>ID: {{ mechanic.id }}</p>
    <p>Workshop: {{ mechanic.workshopId }}</p>
    <p>Status: {{ mechanic.operationalStatus }}</p>
    <p>Availability: {{ mechanic.availabilityStatus }}</p>
    <work-day-section :mechanic-id="mechanic.id" />
    <skill-area-section :mechanic-id="mechanic.id" />
  </div>
</template>

<script setup>
import { defineProps } from 'vue';
import WorkDaySection from './WorkDaySection.vue';
import SkillAreaSection from './SkillAreaSection.vue';

defineProps({ mechanic: Object });
</script>
