<script setup>
import { ref, computed } from "vue";
const assignments = ref([
  { name: "project 1", complete: false, id: 1 },
  { name: "project 2", complete: false, id: 2 },
  { name: "project 3", complete: false, id: 3 },
  { name: "project 4", complete: false, id: 4 },
  { name: "project 5", complete: false, id: 5 },
]);

const inProgressAssignment = computed(() => {
  return assignments.value.filter((a) => !a.complete);
});
const completedAssignment = computed(() => {
  return assignments.value.filter((a) => a.complete);
});
</script>

<template>
  <div class="container mx-auto my-12">
    <section v-if="inProgressAssignment.length">
      <h2>Progressive Value</h2>
      <ul>
        <li v-for="assignment in inProgressAssignment" :key="assignment.id">
          <label
            >{{ assignment.name }}
            <input type="checkbox" v-model="assignment.complete"
          /></label>
        </li>
      </ul>
    </section>

    <section v-if="completedAssignment.length">
      <h2 class="mt-8">Completed</h2>
      <ul>
        <li v-for="assignment in completedAssignment" :key="assignment.id">
          <label
            >{{ assignment.name }}
            <input type="checkbox" v-model="assignment.complete" />
          </label>
        </li>
      </ul>
    </section>
  </div>
</template>

<style scoped></style>
