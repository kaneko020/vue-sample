<script setup lang="ts">
import { ref, reactive, computed, watch } from 'vue';
import { Todo } from '../types/todo';


const todoList = reactive<Todo[]>([
    {
        title: 'Vueの勉強',
        url: 'https://www.udemy.com/share/105XXM3@lkjLaFyLMS4gI0SBTdaj_KcRgRT_Md-52oDUUxEP9QW5CdDDNJJ84r1iYnYf19JKoQ==/',
        summary: '',
    }
])

const onSubmit = () => {

}
</script>

<template>
    <form @submit.prevent="onSubmit" class="todo-form">
        <input type="text" placeholder="TODOを入力" v-model="todoList.title" />
        <input type="text" placeholder="URLを入力" v-model="todoList.url" />
        <textarea type="text" placeholder="備考" v-model="todoList.summary" />
        <button type="submit">追加</button>
    </form>
</template>

<style scoped>
.todo-form {
    display: flex;
    flex-direction: column;
    align-items: center;
    margin: 20px;
}

input {
    width: 800px;
    font-size: 15px;
    padding: 8px;
    border: 1px solid #ddd;
    border-radius: 3px;
    margin-bottom: 10px;
}

textarea {
    width: 800px;
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