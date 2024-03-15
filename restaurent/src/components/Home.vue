<template>
  <h1>Hello user, Welcome to my page</h1>
</template>

<script setup>
import router from "../router";
const name = "Home";
const redirectToSignUpPage = () => {
  router.push({ name: "SignUp" });
};
let user = localStorage.getItem("user-info");
if (!user) {
  redirectToSignUpPage();
}
</script>
