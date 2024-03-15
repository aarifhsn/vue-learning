<script setup>
import { ref, reactive } from "vue";
let friends = ["arif", "marfi", "ayaat", "sathi", "farjana"];
const products = [
  {
    id: 1,
    title:
      "sunt aut facere repellat provident occaecati excepturi optio reprehenderit",
    body: "quia et suscipit\nsuscipit recusandae consequuntur expedita et cum\nreprehenderit molestiae ut ut quas totam\nnostrum rerum est autem sunt rem eveniet architecto",
  },
  {
    id: 2,
    title: "qui est esse",
    body: "est rerum tempore vitae\nsequi sint nihil reprehenderit dolor beatae ea dolores neque\nfugiat blanditiis voluptate porro vel nihil molestiae ut reiciendis\nqui aperiam non debitis possimus qui neque nisi nulla",
  },
  {
    id: 3,
    title: "ea molestias quasi exercitationem repellat qui ipsa sit aut",
    body: "et iusto sed quo iure\nvoluptatem occaecati omnis eligendi aut ad\nvoluptatem doloribus vel accusantium quis pariatur\nmolestiae porro eius odio et labore et velit aut",
  },
  {
    id: 4,
    title: "eum et est occaecati",
    body: "ullam et saepe reiciendis voluptatem adipisci\nsit amet autem assumenda provident rerum culpa\nquis hic commodi nesciunt rem tenetur doloremque ipsam iure\nquis sunt voluptatem rerum illo velit",
  },
  {
    id: 5,
    title: "nesciunt quas odio",
    body: "repudiandae veniam quaerat sunt sed\nalias aut fugiat sit autem sed est\nvoluptatem omnis possimus esse voluptatibus quis\nest aut tenetur dolor neque",
  },
];
</script>

<template>
  <ul>
    <li v-for="friend in friends">{{ friend }}</li>
  </ul>

  <table>
    <tr>
      <th>Name</th>
      <th>Id</th>
      <th>Description</th>
    </tr>

    <tr v-for="(product, index) in products" :key="products.index">
      <td>{{ product.title }}</td>
      <td>{{ product.id }}</td>
      <td>{{ product.body }}</td>
    </tr>
  </table>
</template>

<style scoped>
td,
th {
  border: 1px solid #ddd;
  padding: 4px;
}
</style>
