<script setup>
import { ref, computed } from "vue";

let password = ref("");

const passwordStrength = computed(() => {
  let strength = (password.value.length * 100) / 10;

  return Math.min(strength, 100);
});

let firstName = ref("");
let lastName = ref("");

const fullName = computed(() => {
  let fullNames = firstName.value + " " + lastName.value;
  return fullNames;
});
</script>

<template>
  <input v-model="password" type="password" name="password" id="" />
  {{ passwordStrength }} % stength

  <br />

  <input v-model="firstName" type="text" name="firstName" />
  <input v-model="lastName" type="text" name="firstName" />

  {{ fullName }}
</template>

<style scoped></style>
