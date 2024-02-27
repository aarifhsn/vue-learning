<script setup>
import { reactive } from "vue";

const todos = reactive([
  {
    id: 1,
    title: "TODO ONE",
    completed: true,
  },
  {
    id: 2,
    title: "TODO TWO",
    completed: false,
  },
  {
    id: 3,
    title: "TODO THREE",
    completed: true,
  },
]);
</script>

<template>
  <div
    class="max-w-md mx-auto bg-white shadow-sm rounded overflow-hidden p-4 mt-6 space-y-6"
  >
    <h1 class="font-bold text-2xl my-2">Todo List (02/20)</h1>
    <form>
      <div class="flex border-1 border-slate-500 border-solid">
        <input
          class="border rounded w-full text-slate-700 p-2"
          type="text"
          placeholder="Add a task"
        />
        <button
          class="border px-4 py-2 rounded hover:bg-slate-200"
          type="submit"
        >
          Add
        </button>
      </div>
    </form>
    <div class="todo_items mt-4">
      <ul>
        <li v-for="todo in todos" class="flex justify-between">
          <div>
            <input
              :checked="todo.completed"
              class="mr-2"
              type="checkbox"
              name="todo"
              id="todo"
            />
            <label for="todo"
              ><span>{{ todo.title }}</span></label
            >
          </div>
          <div
            class="delete px-2 py-1 border rounded font-bold hover:border-slate-300"
          >
            X
          </div>
        </li>
      </ul>
    </div>
  </div>
</template>

<style scoped></style>
