<script setup lang="ts">
import { Todo } from '../types/todo';
import { ref } from 'vue';

const todo = ref<Todo>({
    uuid: '',
    title: '',
    summary: ''
})

const emit = defineEmits({
    submit: (todo: Todo) => true
})

// フォーム送信処理
const onSubmit = (value: Todo) => {
    if (value.title) {
        emit('submit', value)
        // フォームリセット
        todo.value = {
            uuid: '',
            title: '',
            summary: ''
        }
    }
}
</script>

<template>
    <div class="accordion">
        <form @submit.prevent="() => onSubmit(todo)" class="todo-form">
            <input type="text" placeholder="TODOを入力" v-model="todo.title" />
            <textarea type="text" placeholder="備考" v-model="todo.summary" />
            <button type="submit">追加</button>
        </form>
    </div>
</template>

<style scoped>
.todo-form {
    display: flex;
    flex-direction: column;
    align-items: center;
    margin: 20px;
}

input, textarea  {
    width: 60%;
    font-size: 15px;
    padding: 8px;
    border: 1px solid #ddd;
    border-radius: 3px;
    margin-bottom: 10px;
}

textarea {
    height: 80px;
}

input:focus, textarea:focus {
    outline: #aaaaaa solid 1px;
}

button {
    width: 80px;
    padding: 8px;
    color: white;
    border: none;
    border-radius: 5px;
    cursor: pointer;
    margin-top: 8px;
    border: #2d8fdd solid 1px;
    transform: translateY(-4px);
    box-shadow: 0 4px 2px #6f95b6;
    background-color: #ffffff;
    color: #1e66a0;
    font-weight: bold;
    font-size: 15px;
}

button:hover {
    transition-duration: 0.3s;
    background-color: #2d8fdd;
    color: white;
}

button:active {
    transition-duration: 0s;
    background-color: #2d8fdd;
    transform: translateY(0px);
    box-shadow: none;
}
</style>