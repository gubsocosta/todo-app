<template>
  <h1>Todo List</h1>
  <ul>
    <li v-for="todo in todoList" :key="todo.id">
      {{ todo.title }}
    </li>
    <input type="text" name="name" v-model="name"/>
  </ul>
</template>

<script>

import {onMounted, ref} from "vue";
import TodoService from "@/services/todo.service";

export default {
  name: 'TodoList',
  setup() {
    const todoList = ref([]);

    onMounted(() => {
      TodoService.getAll()
        .then((response) => todoList.value = response.data)
        .catch((err) => console.log(err));
    });

    return {todoList}
  }
}
</script>
