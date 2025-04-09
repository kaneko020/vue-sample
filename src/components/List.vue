<script setup lang="ts">
import { ref, reactive, watch } from 'vue';

const props = defineProps<{
    todoList: string[]
}>()

</script>

<template>
    <div class="todo-list">
        <ul>
            <li v-for="(todo, index) in props.todoList" :key="index">
                {{ todo }}
                <button @click="deleteTodo(index)">削除</button>
            </li>
        </ul>
    </div>
</template>

<style scoped>

</style>