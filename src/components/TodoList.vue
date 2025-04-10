<script setup lang="ts">
import Form from './Form.vue';
import Header from './Header.vue';
import List from './List.vue';
import Modal from './Modal.vue';
import { Todo } from '../types/todo';
import { ref, reactive } from 'vue';
import { v4 } from 'uuid';

const todoList = reactive<Todo[]>([])

const onSubmit = (todo: Todo) => {
    todo.uuid = v4()
    todoList.push(todo)
}

const emit = defineEmits({
    modal: (todo: Todo) => true
})

const isOpen = ref<boolean>(false)
const modalData = ref<Todo>({
    uuid: '',
    title: '',
    summary: ''
})

const closeModal = () => {
    isOpen.value = false
}

const openModal = (todo: Todo) => {
    isOpen.value = true
    modalData.value = todo
}


const onDelete = (uuid: string) => {
    const index = todoList.findIndex(todo => todo.uuid === uuid)
    if (index !== -1) {
        todoList.splice(index, 1)
    }
}

</script>

<template>
    <div class="container">
        <Header />
        <Form @submit="onSubmit" />
        <List :todoList="todoList" @openModal="openModal" @delete="onDelete" />
    </div>
    <Modal v-if="isOpen" class="modal" :todo="modalData" @closeModal="closeModal" />
    <div v-if="isOpen" class="open-modal" @click="closeModal"></div>
</template>

<style scoped>
.container {
    display: flex;
    flex-direction: column;
    position: relative;
}

.modal {
    position: fixed;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    z-index: 2;
}

.open-modal {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, 0.5);
    z-index: 1;
}

</style>