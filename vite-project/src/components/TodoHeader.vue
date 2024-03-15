<script setup>
import { routerLink } from "vue-router";
</script>

<template>
  <div class="container mx-auto">
    <header>
      <nav>
        <div class="branding">
          <img src="" alt="" />
          <h1>Vue Todos</h1>
        </div>
        <ul class="nav-routes">
          <li><router-link to="/">Home</router-link></li>
        </ul>
      </nav>
    </header>
  </div>
</template>

<style scoped></style>
