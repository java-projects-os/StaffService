<template>
  <div>
    <h2>Mechanics</h2>
    <ul>
      <li v-for="m in mechanics" :key="m.id">
        {{ m.id }} - {{ m.operationalStatus }} - {{ m.availabilityStatus }}
        <button @click="$emit('select', m)">Details</button>
      </li>
    </ul>
  </div>
</template>

<script setup>
defineProps({ mechanics: Array });
</script>
