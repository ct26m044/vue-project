<script setup lang="ts">
import { ref, computed } from 'vue'
import type { Todo } from '../Types'
import TodoList from './TodoList.vue'

const todos = ref<Todo[]>([
  { id: 1, text: 'Task A', done: false },
  { id: 2, text: 'Task B', done: false },
])

const newTodoText = ref('')
const filter = ref<'all' | 'open' | 'done'>('all')

function addTodo() {
  if (!newTodoText.value.trim()) return
  todos.value.push({ id: Date.now(), text: newTodoText.value.trim(), done: false })
  newTodoText.value = ''
}

function toggleTodo(id: number) {
  const todo = todos.value.find((t) => t.id === id)
  if (todo) todo.done = !todo.done
}

function deleteTodo(id: number) {
  todos.value = todos.value.filter((t) => t.id !== id)
}

const filteredTodos = computed(() =>
  todos.value.filter((t) => filter.value === 'all' || (filter.value === 'open') === !t.done)
)

</script>

<template>
  <div class="todo-app">
    <h1>My Todos</h1>

    <form @submit.prevent="addTodo" class="add-form">
      <input v-model="newTodoText" type="text" placeholder="Add new todo..."/>
      <button type="submit">Add</button>
    </form>

    <div class="filters">
      <button :class="{ active: filter === 'all' }" @click="filter = 'all'">All</button>
      <button :class="{ active: filter === 'open' }" @click="filter = 'open'">Open</button>
      <button :class="{ active: filter === 'done' }" @click="filter = 'done'">Done</button>
    </div>

    <TodoList :todos="filteredTodos" @toggle="toggleTodo" @delete="deleteTodo"/>
  </div>

</template>

<style scoped>
.todo-app { max-width: 400px; margin: 2rem auto; font-family: sans-serif; }
.add-form { display: flex; gap: 0.5rem; margin-bottom: 1rem; }
.add-form input { flex: 1; }
.filters { display: flex; gap: 0.5rem; margin-bottom: 1rem; }
.filters button.active { font-weight: bold; text-decoration: underline; }

</style>