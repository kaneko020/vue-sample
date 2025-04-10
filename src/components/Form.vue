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
            <!-- <input type="text" placeholder="URLを入力" v-model="todo.url" /> -->
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

input {
    width: 60%;
    font-size: 15px;
    padding: 8px;
    border: 1px solid #ddd;
    border-radius: 3px;
    margin-bottom: 10px;
}

textarea {
    width: 60%;
    height: 100px;
    font-size: 15px;
    padding: 8px;
    border: 1px solid #ddd;
    border-radius: 3px;
    margin-bottom: 10px;
}

button {
    width: 80px;
    padding: 8px;
    background-color: #386ddf;
    color: white;
    border: none;
    border-radius: 5px;
    cursor: pointer;
}

button:hover {
    background-color: #386ddf;
}
</style>