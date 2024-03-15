<script setup>
import { ref, reactive } from "vue";

const form = reactive({
  email: "",
  password: "",
});
</script>

<template>
  <input type="text" name="email" placeholder="email" v-model="form.email" />
  <input
    type="password"
    name="password"
    placeholder="password"
    v-model="form.password"
  />

  {{ form }}
</template>

<style scoped></style>
