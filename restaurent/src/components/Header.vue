<script setup>
import router from "@/router";
const name = "Header";
const logoutFunction = () => {
  localStorage.clear();
  router.push({ name: "Login" });
};
</script>

<template>
  <div class="nav">
    <ul>
      <li><router-link to="/">Home</router-link></li>
      <li><router-link to="/add">Add Restaurent</router-link></li>
      <li><router-link to="/update">Update Restaurent</router-link></li>
      <li><a href="#" @click="logoutFunction">Logout</a></li>
    </ul>
  </div>
</template>

<style scoped>
.nav {
  background-color: #ede7e7;
  padding: 20px 0;
  width: 100%;
  border: 1px solid #ded5d5;
}
.nav ul[data-v-c970699f] {
  display: flex;
  flex-wrap: wrap;
  gap: 16px;
  list-style: none;
  margin: 0;
}
.nav ul li a {
  text-decoration: none;
  font-weight: 500;
}
</style>
