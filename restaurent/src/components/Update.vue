<script setup>
import router from "../router";
import Header from "./Header.vue";
import axios from "axios";
import { ref } from "vue";

const redirectToSignUpPage = () => {
  router.push({ name: "SignUp" });
};
let user = localStorage.getItem("user-info");
if (!user) {
  redirectToSignUpPage();
}

const restaurent = ref({
  name: "",
  address: "",
  contact: "",
});
</script>

<template>
  <div class="container">
    <Header />
    <h1>Hello user, Welcome to Update Restaurent page</h1>
    <div class="update_form">
      <form>
        <input
          type="text"
          name="name"
          :placeholder="
            restaurent.value ? restaurent.value.name : 'Enter restaurent name'
          "
          v-model="restaurent.name"
        />
        <input
          type="text"
          name="address"
          placeholder="Enter Address"
          v-model="restaurent.address"
        />
        <input
          type="text"
          name="contact"
          placeholder="Enter Contact"
          v-model="restaurent.contact"
        />
        <button @click="addRestaurent" type="button">Update Restaurent</button>
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
