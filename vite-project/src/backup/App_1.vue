<script setup>
let msg = "welcome to vue, arif";

let dynamicId = 2;

let isButtonDisabled = true;

const objectAttr = {
  id: "container",
  class: "wrapper",
};

let seen = false;

const clickMe = () => {
  console.log("button is clicked");
};
</script>

<template>
  <div v-html="msg"></div>
  <div :id="dynamicId">Dynamic ID</div>

  <button :disabled="isButtonDisabled">Button Enable</button>

  <div v-bind="objectAttr">Class Attributes</div>

  <!-- v-if will remove the content from dom if it is false  -->
  <p v-if="seen">Now you see me</p>
  <p v-show="seen">Now you see me 2</p>

  <!-- @click is the shortcut of v-on:click -->
  <button @click="clickMe">Click Me</button>
</template>

<style scoped></style>
