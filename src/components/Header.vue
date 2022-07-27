<script setup>

const props = defineProps({
    currentTheme: String,
})

const appInfo = {
    title: "Todo List",
    description: "Plan now and get a more meaningful life"
};

</script>

<template>
    <header class="app_header">
        <h1 class="main_heading">
            <img src="../assets/images/logo.png" alt="logo" class="high_quality_logo">
            {{ appInfo.title }}
        </h1>
        <button type="button" aria-label="toggle theme" class="toggle_theme_btn" :class="currentTheme + '_theme'"
            @click="$emit('toggleTheme')"></button>
        <h2 class="subtitle">{{ appInfo.description }}</h2>
    </header>
</template>

<style scoped lang="scss">
@import '../assets/partials/variables';
@import '../assets/partials/mixins';

.app_header {
    display: flex;
    justify-content: space-between;
    flex-wrap: wrap;
    .high_quality_logo {
        //dimensions values half of the original to higher resolution display
        width: 27rem;
        height: 27rem;
    }
    .toggle_theme_btn {
        width: 34rem;
        height: 34rem;
        border-radius: 50%;
        border: 2px solid $primary_text_color;

        &.violet_theme {
            @include gradient_btn($light_orchid, $violet_blue);
        }

        &.cabsav_theme {
            @include gradient_btn($careys_pink, $light_tapestry);
        }
    }

    .subtitle {
        position: relative;
        padding-bottom: 19rem;

        &::after {
            content: '';
            position: absolute;
            bottom: 0;
            left: 0;
            width: 33%;
            height: 8rem;
            background-color: $primary_text_color;
            opacity: 0.15;
        }
    }
}

</style>