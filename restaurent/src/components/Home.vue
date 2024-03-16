<script setup>
import router from "../router";
import Header from "./Header.vue";
import { ref } from "vue";
import axios from "axios";

const redirectToSignUpPage = () => {
  router.push({ name: "SignUp" });
};
let user = localStorage.getItem("user-info");
if (!user) {
  redirectToSignUpPage();
}

// Parse user info (assuming it's stored as JSON)
user = JSON.parse(user);

// Extract user's name
const name = ref(user.name);

let restaurent = ref([]);

const fetchData = async () => {
  try {
    let response = await axios.get("http://localhost:3000/restaurent");
    restaurent.value = response.data; // Assign fetched data to restaurent
  } catch (error) {
    console.error(error);
  }
};
fetchData();
</script>

<template>
  <div class="container">
    <Header />
    <h1>Hello {{ name }}, Welcome to my page</h1>
    <div class="restaurent_list">
      <table border="1">
        <tr>
          <td>ID</td>
          <td>NAME</td>
          <td>CONTACT</td>
          <td>ADDRESS</td>
          <td>ACTION</td>
        </tr>
        <tr v-for="item in restaurent" :key="item.id">
          <td>{{ item.id }}</td>
          <td>{{ item.name }}</td>
          <td>{{ item.contact }}</td>
          <td>{{ item.address }}</td>
          <td><router-link :to="'/update/' + item.id">Update</router-link></td>
        </tr>
      </table>
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
.restaurent_list td {
  width: 150px;
  padding: 2px;
}
</style>
