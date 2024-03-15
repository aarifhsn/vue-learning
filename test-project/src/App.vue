<script setup>
import { ref } from "vue";

const count = ref(0);
</script>

<template>
  <a href="#" @click="count++">Click: {{ count }}</a>
</template>

<style scoped></style>
