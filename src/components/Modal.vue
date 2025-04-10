<script setup lang="ts">
import { Todo } from '../types/todo';

const props = defineProps<{
    todo: Todo
}>()

const emit = defineEmits({
    closeModal: () => true
})

const closeModal = () => {
    emit('closeModal')
}

</script>

<template>
    <div class="modal-wrapper">
        <div class="modal-header">
            <div class="modal-title">TODO 詳細</div>
            <button class="close" @click="() => closeModal()">&times;</button>
        </div>
        <div class="modal-content">
            <p class="todo-title">{{ props.todo.title }}</p>
            <p>備考：{{ props.todo.summary }}</p>
        </div>
    </div>
</template>

<style scoped>
.modal-wrapper {
    width: 60%;
    max-height: 40%;
    overflow: scroll;
    background-color: #f7f7f7;
    border-radius: 5px;
}

.modal-header {
    display: flex;
    padding-right: 10px;
    background-color: #e0e0e0;
}

.modal-header .modal-title {
    flex: 1;
    pointer-events: all;
    font-size: 18px;
    font-weight: bold;
    color: black;
    justify-content: center;
    padding: 5px 20px;
}

.modal-header .close {
    font-size: 24px;
    color: black;
    text-decoration: none;
    cursor: pointer;
}

.modal-content {
    padding: 17px;
    pointer-events: all;
    color: black;
}

.todo-title {
    font-size: 17px;
    font-weight: bold;
}

button {
    direction: none;
    background: none;
    border: none;
    color: inherit;
    font: inherit;
}
</style>