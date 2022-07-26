<script setup>
import { reactive, watchEffect } from 'vue'
import TodoItem from './TodoItem.vue';
import AddTaskForm from './AddTaskForm.vue';

const local_data_key = 'localTodoList';
const todoList = reactive([]);

//get data from local storage if exists
todoList.value = JSON.parse(localStorage.getItem(local_data_key)) ?? []



/*
** 1- move uncompleted task to the top
** 2- move completed task to the end
*/
function toggleTaskState(task) {
    deletetask(task)

    if(task.done) {
        todoList.value.push(task)
    } else {
        todoList.unshift.value(task)
    }
}

/*
** delete task permanently
** affected the original array
*/
function deletetask(task) {
    let taskIndex = todoList.value.indexOf(task);
    todoList.value.splice(taskIndex, 1);
}

//add new task
function addNewTask(task) {
    let taskObject = {
        id: todoList.value.length + 1,
        title: task,
        done: false
    }

    todoList.value.unshift(taskObject);
}


//update local storage item on todoList changed
watchEffect(() => {
    localStorage.setItem(local_data_key, JSON.stringify(todoList.value))
})

</script>

<template>
    <section class="todo_list_conatiner">
        <h3 class="title">0/3 done</h3>
        <!-- todo items -->
        <transition-group tag="ul" name="list">
            <TodoItem v-for="item in todoList.value" :taskDetails="item" :key="item.id"
                @stateChanged="toggleTaskState(item)" @deleteTask="deletetask(item)">
            </TodoItem>
        </transition-group>

        <!-- add todo item form -->
        <AddTaskForm @newTaskAdded="addNewTask"></AddTaskForm>

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