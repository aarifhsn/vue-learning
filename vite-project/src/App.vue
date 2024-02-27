<script setup>
import { reactive, ref, computed } from "vue";

let todo = ref("");
const todos = reactive([
  {
    id: 1,
    title: "Learn Vue",
    completed: false,
  },
]);

const checkCompleted = (index) => {
  todos[index].completed = !todos[index].completed;
};

const removeTodo = (index) => {
  todos.splice(index, 1);
};

const addTodo = () => {
  if (todo.value.trim() === "") {
    alert("Please, Input a value");
    return;
  }

  todos.push({
    id: todos.length + 1,
    title: todo.value,
    completed: false,
  });

  todo.value = "";
};

const countAllTodos = computed(() => {
  return todos.length;
});

const countCompletedTodos = computed(() => {
  return todos.filter((todo) => todo.completed).length;
});
</script>

<template>
  <div
    class="max-w-md mx-auto bg-white shadow-sm rounded overflow-hidden p-4 mt-6 space-y-6"
  >
    <h1 class="font-bold text-2xl my-2">
      Todo List
      <span v-if="todos.length"
        >({{ countCompletedTodos }} / {{ countAllTodos }})</span
      >
    </h1>
    <form @submit.prevent="addTodo">
      <div class="flex border-1 border-slate-500 border-solid">
        <input
          v-model="todo"
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
      <ul v-if="todos.length">
        <li
          v-for="(todo, index) in todos"
          :key="todo.id"
          class="flex justify-between"
        >
          <div>
            <input
              @input="checkCompleted(index)"
              :checked="todo.completed"
              class="mr-2"
              type="checkbox"
              name="todo"
              :id="`todo-${todo.id}`"
            />
            <label
              :class="{ 'line-through': todo.completed }"
              :for="`todo-${todo.id}`"
              ><span>{{ todo.title }}</span></label
            >
          </div>
          <div
            @click="removeTodo(index)"
            class="delete px-2 py-.5 my-1 border rounded font-bold hover:border-slate-300 cursor-pointer"
          >
            X
          </div>
        </li>
      </ul>
      <div v-else class="no_task">
        <p class="text-red-800 font-semibold">No task is added</p>
      </div>
    </div>
  </div>
</template>

<style scoped></style>
