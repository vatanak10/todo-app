<template>
  <form @submit.prevent="addTodoAndReset">
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
</template>

<script lang="ts" setup>
const todo = ref<string>("");
const emit = defineEmits(["submit"]);

function addTodoAndReset() {
  emit("submit", todo.value);
  todo.value = "";
}
</script>
