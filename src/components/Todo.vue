<script setup lang="ts">
import Header from './Header.vue';
import Form from './Form.vue';
import List from './List.vue';
import { ref, reactive, computed, watch } from 'vue';

const todoList = reactive<string[]>([])

</script>

<template>
    <div class="container">
        <Header />
        <Form />
        <List :todoList="todoList" />
    </div>
</template>

<style scoped>
.container {
    display: flex;
    flex-direction: column;
}

</style>