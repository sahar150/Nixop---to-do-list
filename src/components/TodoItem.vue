<script setup>

const props = defineProps({
    taskDetails: {
        id: Number,
        title: String,
        done: Boolean
    }

})

</script>

<template>
    <li class="task_container">
        <label :for="'task' + props.taskDetails.id" class="to_do_item" :class="{ done: props.taskDetails.done }">
            <input type="checkbox" :id="'task' + props.taskDetails.id" v-model="props.taskDetails.done" @change="$emit('stateChanged')"/>
            <span class="task_title">{{ props.taskDetails.title}}</span>
        </label>

        <button class="icon_btn" type="button" aria-label="delete task">
            <!-- TODO: use svg object instead image -->
            <img src="../assets/images/delete.svg" alt="">
        </button>
    </li>
</template>

<style scoped lang="scss">

@import '../assets/variables';

.task_container {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 12rem;

    .to_do_item {
        display: flex;
        width: calc(100% - 38px); // 38px = delete button width + gap
        padding: 19rem;
        border-radius: $element_border_radius;
        cursor: pointer;
        //same color for both themes
        background-color: rgba($selago, 0.14);

        .task_title {
            overflow: hidden;
            text-overflow: ellipsis;
            display: -webkit-box;
            -webkit-line-clamp: 1;
            -webkit-box-orient: vertical;
        }

        //custom checkbox style
        input[type="checkbox"] {
            -webkit-appearance: none;
            appearance: none;
            position: relative;
            width: 18.5rem;
            height: 18.5rem;
            margin-inline-end: 18.5rem;

            &::after {
                content: url('../assets/images/checkbox.svg');
                position: absolute;
                top: 0;
                left: 0;
            }
        }

        &.done {
            input[type="checkbox"]::after {
                content: url('../assets/images/checkbox_done.svg');
            }
        }
    }

    .icon_btn {
        cursor: pointer;
    }

}

</style>