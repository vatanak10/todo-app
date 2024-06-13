<template>
  <div class="mt-4">
    <div class="text-lg font-semibold">Todo List</div>

    <div class="mb-2 border-b border-gray-300"></div>

    <TodoCard
      v-for="item in todoList"
      :key="item.id"
      :value="item"
      class="mt-2"
      @removeTodo="removeTodo"
    />
  </div>
</template>

<script lang="ts" setup>
import type { TodoItem } from "~/types/index";
const todoList = defineModel("items") as Ref<TodoItem[]>;

function removeTodo(id: number) {
  todoList.value = todoList.value.filter((t: TodoItem) => t.id !== id);
}
</script>
