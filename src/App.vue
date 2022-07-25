<script setup>
import { ref } from 'vue'

//import components
import Header from './components/Header.vue';

const availabelThemes = ['violet', 'cabsav'];
const currentTheme = ref(availabelThemes[0]);

//toggle them function
function toggleTheme() {
    //TODO: refactore  to handle more than two themes
    currentTheme.value = currentTheme.value === availabelThemes[0] ? availabelThemes[1] : availabelThemes[0]
}

</script>

<template>
    <main class="main_container" :class="currentTheme + '_theme'">
        <Header :currentTheme="currentTheme" @toggleTheme="toggleTheme"></Header>
    </main>
</template>

<style scoped lang="scss">

@import './assets/variables';
@import './assets/mixins';
    .main_container {
        position: relative;
        width: 95%;
        max-width: 456px;
        min-height: 70vh;
        border-radius: $container_border_radius;
        padding: 28rem;

        //outer container gradiant background without adding extra unnecessary html tag
        &::before {
            content: '';
            position: fixed;
            top: 0;
            left: 0;
            width: 100vw;
            height: 100vh;
            z-index: -1;
        }

        &.violet_theme {
            &::before {
                @include outer_container_bg($light_lilac, $sunff_approx);
            }

            @include inner_container_style($light_orchid, $violet_blue, $venice);
        }

        &.cabsav_theme {
            &::before {
                @include outer_container_bg($amourapprox, $prim);
            }

            @include inner_container_style($careys_pink, $light_tapestry, $dark_tapestry);
        }

    }
</style>
