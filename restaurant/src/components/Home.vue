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

let restaurant = ref([]);

const fetchData = async () => {
  try {
    let response = await axios.get("http://localhost:3000/restaurant");
    restaurant.value = response.data; // Assign fetched data to restaurant
  } catch (error) {
    console.error(error);
  }
};
fetchData();

const deleteRestaurant = async (id) => {
  try {
    await axios.delete(`http://localhost:3000/restaurant/${id}`);
    // Remove the deleted item from the restaurant list
    restaurant.value = restaurant.value.filter((item) => item.id !== id);
    console.log("Restaurant deleted successfully.");
  } catch (error) {
    console.error("Error deleting restaurant:", error);
  }
};
const confirmDelete = (id) => {
  if (window.confirm("Are you sure you want to delete this restaurant?")) {
    deleteRestaurant(id);
  }
};
</script>

<template>
  <div class="container">
    <Header />
    <h1>Hello {{ name }}, Welcome to my page</h1>
    <div v-if="restaurant.length" class="restaurant_list">
      <table border="1">
        <tr>
          <td>ID</td>
          <td>NAME</td>

          <td>ADDRESS</td>
          <td>CONTACT</td>
          <td>ACTION</td>
        </tr>
        <tr v-for="item in restaurant" :key="item.id">
          <td>{{ item.id }}</td>
          <td>{{ item.name }}</td>

          <td>{{ item.address }}</td>
          <td>{{ item.contact }}</td>
          <td class="action">
            <router-link :to="'/update/' + item.id">Update</router-link>
            <p @click="confirmDelete(item.id)">Delete</p>
          </td>
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
.restaurant_list td {
  width: 150px;
  padding: 2px;
}
td.action {
  display: flex;
  gap: 16px;
  justify-content: space-between;
  padding: 0 4px;
}
td.action p {
  margin: 0;
  padding: 0;
  cursor: pointer;
}
</style>
