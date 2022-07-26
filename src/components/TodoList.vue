<script setup>
import { reactive } from 'vue'
import TodoItem from './TodoItem.vue';

const todoList = reactive([
    {
        id: 1,
        title: 'task titlehguihioh nojhio j;oi oiujoikj oiuoiu iouiou ',
        done: false
    },
    {
        id: 2,
        title: 'task title',
        done: false
    },
    {
        id: 3,
        title: 'task title',
        done: false
    },
])

</script>

<template>
    <section class="todo_list_conatiner">
        <h3 class="title">0/3 done</h3>
        <transition-group tag="ul">
            <TodoItem v-for="item in todoList" :taskDetails="item" :key="item.id"></TodoItem>
        </transition-group>

    </section>
</template>

<style scoped lang="scss">
.todo_list_conatiner {
    padding-block: 42rem;

    .title {
        margin-bottom: 20rem;
    }
}
</style>