<template>
  <div class="container mx-auto mt-4 max-w-sm px-2 text-gray-700">
    <div class="text-center text-lg font-semibold">My Simple Todo App</div>
    <form @submit="addTodo">
      <label class="mb-1 block text-xs" for="todo-field"> New Todo </label>
      <input
        v-model="todo"
        class="focus:shadow-outline w-full appearance-none rounded border px-3 py-2 leading-tight shadow focus:outline-none"
        id="todo-field"
        type="text"
        placeholder="Todo"
      />
      <button
        type="submit"
        class="focus:shadow-outline mt-2 block w-full rounded bg-blue-500 py-1 text-white transition-all duration-200 hover:bg-blue-600 focus:outline-none"
      >
        Add Todo
      </button>
    </form>

    <!-- Todo List -->
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
  </div>
</template>

<script lang="ts" setup>
import type { TodoItem } from "~/types/index";

useSeoMeta({
  title: "My Simple Todo App",
});

const todo = ref<string>("");
const todoList = ref<TodoItem[]>([]);

watch(
  todoList,
  () => {
    updateTodoList();
  },
  { deep: true },
);

function addTodo(event: Event) {
  event.preventDefault();
  if (!todo.value.trim()) return;

  const newTodo: TodoItem = {
    id: Date.now(),
    name: todo.value.trim(),
    checked: false,
  };
  todoList.value.push(newTodo);
  todo.value = "";
}

function removeTodo(id: number) {
  todoList.value = todoList.value.filter((t: TodoItem) => t.id !== id);
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
