<script setup>
import axios from "axios";
import router from "../router";
import { ref } from "vue";
const email = ref("");
const password = ref("");

const loginFunction = async () => {
  try {
    let result = await axios.get(
      `http://localhost:3000/user?email=${email.value}&password=${password.value}`
    );
    if (result.status == 200 && result.data.length > 0) {
      localStorage.setItem("user-info", JSON.stringify(result.data[0]));
      redirectToHomePage();
    }
  } catch (error) {
    console.error("Error during login:", error);
    // Handle the error appropriately, e.g., display a message to the user
  }
};
const redirectToHomePage = () => {
  router.push({ name: "Home" });
};

let user = localStorage.getItem("user-info");
if (user) {
  redirectToHomePage();
}
</script>

<template>
  <div class="container">
    <img class="logo" src="../assets/logo.png" alt="" />
    <h1>Login Page</h1>

    <div class="loginForm">
      <input type="email" name="email" v-model="email" placeholder="Email" />
      <input
        type="password"
        name="password"
        v-model="password"
        placeholder="password"
      />
      <button @click="loginFunction">Login</button>

      <button><router-link to="/sign-up">Sign Up</router-link></button>
    </div>
  </div>
</template>

<style scoped>
.container {
  max-width: 840px;
  margin: 0 auto;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
.logo {
  width: 100px;
  margin-top: 24px;
}
h1 {
  font-size: 20px;
}
.loginForm {
  display: flex;
  flex-direction: column;
}
.loginForm input {
  margin-top: 10px;
  width: 250px;
  border-radius: 4px;
  border: 1px solid #ddd;
  height: 30px;
  padding: 0 4px;
}
.loginForm button {
  margin-top: 10px;
  height: 30px;
  cursor: pointer;
}
</style>
