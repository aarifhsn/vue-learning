<script setup>
import { ref, reactive } from "vue";

import useNumbers from "./numbers";

let number = ref(0);

const { increment, decrement } = useNumbers(number);
</script>

<template>
  <div>
    <button @click="increment">Increment</button>

    <button @click="decrement">Decrement</button>
    {{ number }}
  </div>
</template>

<style scoped></style>
