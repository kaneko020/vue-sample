<script setup lang="ts">
import { Todo } from '../types/todo';

const props = defineProps<{
    todoList: Todo[]
}>()

const emit = defineEmits({
    delete: (uuid: string) => true,
    openModal: (todo: Todo) => true
})

const openModal = (todo: Todo) => {
    emit('openModal', todo)
}

const onDelete = (uuid: string) => {
    emit('delete', uuid)
}

</script>

<template>
    <ul class="todo-list">
        <li v-for="(todo, index) in props.todoList" :key="index">
            <div class="todo-item">
                <p class="title">{{ todo.title }}</p>
                <!-- <p>{{ todo.url }}</p>
                <p>{{ todo.summary }}</p> -->
                <div class="button-group">
                    <button @click="() => openModal(todo)">詳細</button>
                    <button @click="() => onDelete(todo.uuid)">削除</button>
                </div>
            </div>
        </li>
    </ul>
</template>

<style scoped>
.todo-list {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    margin: 20px;
}

.todo-item {
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    align-items: center;
    width: 100%;
    padding: 2px;
}

.title {
    font-size: 16px;
    color: #2d8fdd;
    font-weight: bold;
}

button {
    margin-left: 10px;
    border: none;
    border-radius: 5px;
    padding: 4px 10px;
    cursor: pointer;
    background-color: #2d8fdd;
    color: white;
}

button:hover {
    background-color: #1e66a0;
}

ul {
    list-style: none;
    padding: 0;
}

ul li {
    color: #2d8fdd;
    border-left: solid 6px #2d8fdd;
    background: #f1f8ff;
    margin-bottom: 5px;
    line-height: 1.5;
    padding: 4px 10px;
    width: 60%;
}


</style>