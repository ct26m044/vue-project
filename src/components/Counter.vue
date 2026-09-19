<script setup lang="ts">
import { ref, computed } from 'vue'

const count = ref(0)
const doubled = computed(() => count.value * 2)

function add() {
    count.value = count.value + 1
}

function minus() {
    count.value = count.value - 1
}

</script>

<template>
<p>{{ count }} Single</p>
<p>{{ doubled }} Doubled</p>
<button @click="add">Add +1</button>
<button @click="minus">Minus -1</button>

</template>

<style scoped>
button {
    padding: 4px 8px;
    font-size: 1rem;
    cursor: pointer;
}
</style>