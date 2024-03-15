<script setup>
import { ref, reactive } from "vue";

const form = reactive({
  name: "arif",
  password: 1234,
});

let name = ref("arif hassan");

// let number = ref(0);

// setInterval(() => {
//   number.value++;
// }, 1000);
</script>

<template>
  {{ form.name }} {{ form.password }}
  <!-- {{ number }} -->

  <div>
    <input type="text" v-model="name" />
    <p>{{ name }}</p>
  </div>
</template>

<style scoped></style>
