<script setup lang="ts">
import type { Todo } from '../Types'

defineProps<{ todo: Todo }>()
defineEmits<{ toggle: [id: number]; delete: [id: number] }>()

</script>

<template>
  <li class="todo-item">
    <input type="checkbox" :checked="todo.done" @change="$emit('toggle', todo.id)"/>
    <span :class="{ done: todo.done }">{{ todo.text }}</span>
    <button @click="$emit('delete', todo.id)">Delete</button>
  </li>

</template>

<style scoped>
.todo-item { display: flex; align-items: center; gap: 0.5rem; padding: 0.25rem 0; }
.done { text-decoration: line-through; color: #888; }
button { margin-left: auto; }

</style>