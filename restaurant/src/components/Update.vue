<script setup>
import router from "../router";
import { useRoute } from "vue-router";
import Header from "./Header.vue";
import axios from "axios";
import { ref, onMounted } from "vue";

const redirectToSignUpPage = () => {
  router.push({ name: "SignUp" });
};
let user = localStorage.getItem("user-info");
if (!user) {
  redirectToSignUpPage();
}
const route = useRoute();

const updateResult = async () => {
  let result = await axios.get(
    `http://localhost:3000/restaurant/${route.params.id}`
  );
  restaurant.value = result.data;
};

onMounted(() => {
  updateResult(); // Fetch update result when component is mounted
});

const updateRestaurant = async () => {
  // Check if name and address are provided
  if (!restaurant.value.name || !restaurant.value.address) {
    alert("Name and address are required.");
    return; // Stop execution if validation fails
  }
  try {
    let response = await axios.put(
      `http://localhost:3000/restaurant/${route.params.id}`,
      {
        name: restaurant.value.name,
        address: restaurant.value.address,
        contact: restaurant.value.contact,
      }
    );

    // Redirect to Home page
    if (response.status == 200) {
      router.push({ name: "Home" });
    }
    console.log("Restaurant added successfully:", response.data);
  } catch (error) {
    console.error("Error adding restaurant:", error);
  }
};

const restaurant = ref({
  name: "",
  address: "",
  contact: "",
});
</script>

<template>
  <div class="container">
    <Header />
    <h1>Hello user, Welcome to Update restaurant page</h1>
    <div class="update_form">
      <form>
        <input
          type="text"
          name="name"
          placeholder="Enter restaurant name"
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
        <button @click="updateRestaurant" type="button">
          Update restaurant
        </button>
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
}
.update_form form {
  display: flex;
  flex-direction: column;
}
.update_form form input,
form button {
  margin-top: 10px;
}
</style>
