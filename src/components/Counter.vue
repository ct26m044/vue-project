<script setup lang="ts">
import { ref, computed } from 'vue'

const count = ref(0)
const doubled = computed(() => count.value * 2)
const tripled = computed(() => count.value * 3)

function add() {
    count.value = count.value + 1
}

function minus() {
    count.value = count.value - 1
}

function reset() {
    count.value = 0
}

</script>

<template>
<p>{{ count }} Single</p>
<p>{{ doubled }} Doubled</p>
<p>{{ tripled }} Tripled</p>
<button @click="add">Add +1</button>
<button @click="minus">Minus -1</button>
<button @click="reset">Reset</button>

</template>

<style scoped>
button {
    padding: 4px 8px;
    font-size: 1rem;
    cursor: pointer;
}
</style>