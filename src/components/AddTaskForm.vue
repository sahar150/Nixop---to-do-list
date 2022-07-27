<script setup>
import { ref } from 'vue';

const taskInputValue = ref('');
const emit = defineEmits(['newTaskAdded']);

/*
** 1- trim whitespaces
** 2- emit to parent
*/
function validate() {
    let trimedVal = taskInputValue.value.trim();

    if (trimedVal) {
        emit('newTaskAdded', trimedVal);
        taskInputValue.value = '';
    }
}

</script>

<template>
    <form @submit.prevent="validate">
        <legend class="hint_text">Add new item</legend>
        <div class="form_group">
            <input type="text" placeholder="Write Here" class="hint_text theme_based" v-model="taskInputValue"
                @keyup.enter="validate">
            <button type="submit" class="main_button">ADD</button>
        </div>
    </form>
</template>

<style scoped lang="scss">

@import '../assets/partials/variables';

form {
    margin-top: 32rem;

    .form_group {
        display: flex;
        margin-top: 20rem;

        >* {
            border-radius: $element_border_radius;
        }

        input {
            height: 48rem;
            padding-inline: 16rem;
            width: 100%;
            flex: 1;
        }

        .main_button {
            min-width: 103rem;
            height: 48rem;
            margin-inline-start: 12rem;
            text-align: center;
        }
    }


}

//theming
.violet_theme {
    input {
        background-color: rgba($selago, 0.8);
    }

    .main_button {
        background-color: rgba($selago, 0.14);
    }
}

.cabsav_theme {
    input {
        background-color: rgba($azalea, 0.8);
    }

    .main_button {
        background-color: rgba($azalea, 0.14);
    }
}

</style>