<script setup>

const copyrightsText = 'All Rights Reserved';
const currentYear = new Date().getFullYear();

</script>

<template>
    <footer class="hint_text">
        {{ copyrightsText + ' ' + currentYear + '.'}}
    </footer>
</template>