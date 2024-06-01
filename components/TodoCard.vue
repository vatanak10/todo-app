<template>
  <div
    class="todo-card flex items-center justify-between rounded border p-2 pr-4"
  >
    <div class="flex items-center">
      <div class="mr-2 flex items-center">
        <label
          class="relative flex cursor-pointer items-center rounded-full p-3"
          :for="`checkbox-${value.id}`"
          data-ripple-dark="true"
        >
          <input
            type="checkbox"
            class="before:content[''] border-blue-gray-200 before:bg-blue-gray-500 peer relative h-5 w-5 cursor-pointer appearance-none rounded-md border transition-all before:absolute before:left-2/4 before:top-2/4 before:block before:h-12 before:w-12 before:-translate-x-2/4 before:-translate-y-2/4 before:rounded-full before:opacity-0 before:transition-opacity checked:border-blue-500 checked:bg-blue-500 checked:before:bg-blue-500 hover:before:opacity-10"
            :id="`checkbox-${value.id}`"
            checked
            v-model="value.checked"
          />
          <div
            class="pointer-events-none absolute left-2/4 top-2/4 -translate-x-2/4 -translate-y-2/4 text-white opacity-0 transition-opacity peer-checked:opacity-100"
          >
            <svg
              xmlns="http://www.w3.org/2000/svg"
              class="h-3.5 w-3.5"
              viewBox="0 0 20 20"
              fill="currentColor"
              stroke="currentColor"
              stroke-width="1"
            >
              <path
                fill-rule="evenodd"
                d="M16.707 5.293a1 1 0 010 1.414l-8 8a1 1 0 01-1.414 0l-4-4a1 1 0 011.414-1.414L8 12.586l7.293-7.293a1 1 0 011.414 0z"
                clip-rule="evenodd"
              ></path>
            </svg>
          </div>
        </label>
      </div>
      <label
        :for="`checkbox-${value.id}`"
        class="cursor-pointer"
        :class="{
          'line-through': value.checked,
        }"
      >
        {{ value.name }}
      </label>
    </div>
    <SvgRemoveIcon
      class="svg-remove-icon cursor-pointer text-red-500 opacity-0 transition-all duration-200 ease-in-out"
      @click="$emit('remove-todo', value.id)"
    />
  </div>
</template>

<script lang="ts" setup>
/* __placeholder__ */
import type { TodoItem } from "~/types/index";

const props = defineProps<{
  value: TodoItem;
}>();
</script>

<style scoped>
/* hide Remove icon on hover on .todo-card */
.todo-card:hover .svg-remove-icon {
  opacity: 1;
}
</style>
