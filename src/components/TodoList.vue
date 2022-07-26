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

/*
** 1- move uncompleted task to the top
** 2- move completed task to the end
*/
function toggleTaskState(task) {
    let taskIndex = todoList.indexOf(task);
    //affected the original array
    todoList.splice(taskIndex, 1);

    if(task.done) {
        todoList.push(task)
    } else {
        todoList.unshift(task)
    }
}

</script>

<template>
    <section class="todo_list_conatiner">
        <h3 class="title">0/3 done</h3>
        <transition-group tag="ul" name="list">
            <TodoItem v-for="item in todoList" :taskDetails="item" :key="item.id" @stateChanged="toggleTaskState(item)">
            </TodoItem>
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

//transition styles
.list-enter-active,
.list-leave-active {
    transition: all 0.5s ease;
}

.list-enter-from,
.list-leave-to {
    opacity: 0;
    transform: translateX(30px);
}
.list-move,
/* apply transition to moving elements */
.list-enter-active,
.list-leave-active {
    transition: all 0.5s ease;
}

.list-enter-from,
.list-leave-to {
    opacity: 0;
    transform: translateX(30px);
}

/* ensure leaving items are taken out of layout flow so that moving
   animations can be calculated correctly. */
.list-leave-active {
    position: absolute;
}
</style>