<script setup>
import { defineProps } from "vue";
const props = defineProps({
  index: {
    type: Number,
  },
  todo: {
    type: Object,
  },
});
const checkCompleted = (index) => {
  console.log(index);
};

const removeTodo = (index) => {
  console.log(index);
};
</script>

<template>
  <div>
    <input
      @input="checkCompleted(index)"
      :checked="todo.completed"
      class="mr-2"
      type="checkbox"
      name="todo"
      :id="`todo-${todo.id}`"
    />
    <label :class="{ 'line-through': todo.completed }" :for="`todo-${todo.id}`"
      ><span>{{ todo.title }}</span></label
    >
  </div>
  <div
    @click="removeTodo(index)"
    class="delete px-2 py-.5 my-1 border rounded font-bold hover:border-slate-300 cursor-pointer"
  >
    X
  </div>
</template>
