<script setup>
import { ref } from "vue";
import axios from "axios";
import router from "../router";
const name = ref("");
const email = ref("");
const password = ref("");

const signUpTest = async () => {
  try {
    let result = await axios.post("http://localhost:3000/user", {
      email: email.value,
      name: name.value,
      password: password.value,
    });
    console.log(result);
    if (result.status == 201) {
      localStorage.setItem("user-info", JSON.stringify(result.data));
      redirectToHomePage();
    }
  } catch (error) {
    console.error("Error during sign up:", error);
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
    <h1>SignUp Page</h1>

    <div class="signupForm">
      <input type="text" name="name" v-model="name" placeholder="User Name" />
      <input type="email" name="email" v-model="email" placeholder="Email" />
      <input
        type="password"
        name="password"
        v-model="password"
        placeholder="password"
      />
      <button @click="signUpTest">Sign Up</button>
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
.signupForm {
  display: flex;
  flex-direction: column;
}
.signupForm input {
  margin-top: 10px;
  width: 250px;
  border-radius: 4px;
  border: 1px solid #ddd;
  height: 30px;
  padding: 0 4px;
}
.signupForm button {
  margin-top: 10px;
  height: 30px;
  cursor: pointer;
}
</style>
