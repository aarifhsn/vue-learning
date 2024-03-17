<script setup>
import axios from "axios";
import router from "../router";
import Header from "./Header.vue";
import { ref } from "vue";
const redirectToSignUpPage = () => {
  router.push({ name: "SignUp" });
};
let user = localStorage.getItem("user-info");
if (!user) {
  redirectToSignUpPage();
}

const restaurant = ref({
  name: "",
  address: "",
  contact: "",
});

const addrestaurant = async () => {
  // Check if name and address are provided
  if (!restaurant.value.name || !restaurant.value.address) {
    alert("Name and address are required.");
    return; // Stop execution if validation fails
  }
  try {
    let response = await axios.post("http://localhost:3000/restaurant", {
      name: restaurant.value.name,
      address: restaurant.value.address,
      contact: restaurant.value.contact,
    });

    // Redirect to Home page
    if (response.status == 201) {
      router.push({ name: "Home" });
    }
    console.log("Restaurant added successfully:", response.data);
  } catch (error) {
    console.error("Error adding restaurant:", error);
  }
};
</script>

<template>
  <div class="container">
    <Header />
    <h1>Hello user, Welcome to Add restaurant page</h1>
    <div class="add_form">
      <form>
        <input
          type="text"
          name="name"
          placeholder="Enter Name"
          v-model="restaurant.name"
        />
        <input
          type="text"
          name="address"
          placeholder="Enter Address"
          v-model="restaurant.address"
        />
        <input
          type="text"
          name="contact"
          placeholder="Enter Contact"
          v-model="restaurant.contact"
        />
        <button @click="addrestaurant" type="button">Add New restaurant</button>
      </form>
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
  background-color: #f2eaea;
}
.add_form form {
  display: flex;
  flex-direction: column;
}
.add_form form input,
form button {
  margin-top: 10px;
}
</style>
