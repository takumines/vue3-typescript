<script setup lang="ts">
import { provide } from "vue";
import TodoList from "./components/TodoList.vue";
import {todoKey, todos} from "./useTodo";

// provideを使ってtodosをどこからでも受け取れるよう定義
// inject('todos')で受け取れる
// provide('todos', todos)
provide(todoKey, todos)

</script>

<template>
  <TodoList />
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
