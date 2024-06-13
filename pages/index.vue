<template>
  <div class="container mx-auto mt-4 max-w-sm px-2 text-gray-700">
    <div class="text-center text-lg font-semibold">My Simple Todo App</div>

    <TodoForm @submit="addTodo" />

    <TodoList v-model:items="todoList" />
  </div>
</template>

<script lang="ts" setup>
import type { TodoItem } from "~/types/index";

useSeoMeta({
  title: "My Simple Todo App",
});

const todoList = ref<TodoItem[]>([]);

watch(todoList, () => updateTodoList(), { deep: true });

function addTodo(todo: string) {
  if (!todo.trim()) return;

  const newTodo: TodoItem = {
    id: Date.now(),
    name: todo.trim(),
    checked: false,
  };
  todoList.value.push(newTodo);
}

function updateTodoList() {
  // sort the todo list by id but unchecked todo will be at the top
  todoList.value.sort((a: TodoItem, b: TodoItem) => {
    if (a.checked && !b.checked) return 1;
    if (!a.checked && b.checked) return -1;
    return a.id - b.id;
  });
  localStorage.setItem("todos", JSON.stringify(todoList.value));
}

onMounted(() => {
  const todos = localStorage.getItem("todos");
  todoList.value = todos ? JSON.parse(todos) : [];
});
</script>
