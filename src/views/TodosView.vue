<script setup>
import { ref } from "vue";
import { uid } from "uid";
import { Icon } from '@iconify/vue';

import ToDoCreator from '../components/ToDoCreator.vue';
import ToDoItem from "../components/ToDoItem.vue";

const todoList = ref([]);

const createToDo = (todo) => {
  todoList.value.push({
    id: uid(),
    todo,
    isCompleted: false,
    isEditing: null,
  });
};

const toggleToDoComplete = (todoPos) => {
  todoList.value[todoPos].isCompleted = !todoList.value[todoPos].isCompleted
}

</script>

<template>
  <main>
    <h1>Create ToDo</h1>
    <ToDoCreator @create-todo="createToDo"/>
    <ul class="todo-list" v-if="todoList.length > 0">
      <ToDoItem v-for="(todo, index) in todoList" :todo="todo" :index = "index" @toggle-complete="toggleToDoComplete"/>
    </ul>
    <p class="todos-msg" v-else>
      <Icon icon="noto-v1:sad-but-relieved-face" />
      <span>You have no todo's to complete: Add one!</span>
    </p>
  </main>
</template>

<style>
main {
  display: flex;
  flex-direction: column;
  max-width: 500px;
  width: 100%;
  margin: 0 auto;
  padding: 40px 16px;

  h1 {
    margin-bottom: 16px;
    text-align: center;
  }

  .todo-list {
    display: flex;
    flex-direction: column;
    list-style: none;
    margin-top: 24px;
    gap: 20px;
  }

  .todos-msg {
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 8px;
    margin-top: 24px;
  }
}
</style>
