<script setup lang="ts">
import type { Todo } from '../Types'
import TodoItem from './TodoItem.vue'

defineProps<{
  todos: Todo[]
}>()

const emit = defineEmits<{
  toggle: [id: number]
  delete: [id: number]
}>()

</script>

<template>
  <ul class="todo-list">
    <TodoItem
      v-for="todo in todos"
      :key="todo.id"
      :todo="todo"
      @toggle="emit('toggle', $event)"
      @delete="emit('delete', $event)"
    />
  </ul>

</template>

<style scoped>
.todo-list {
  list-style: none;
  padding: 0;
  margin: 0;
}

</style>