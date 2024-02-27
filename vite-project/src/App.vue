<script setup>
import { ref, computed } from "vue";

const zip = ref("");

const zipUpperCase = computed({
  set: () => zip.value,
  get: () => zip.value.toUpperCase(),
});
</script>

<template>
  <input v-model="zip" type="text" name="name" id="" />
  {{ zipUpperCase }}
</template>

<style scoped></style>
