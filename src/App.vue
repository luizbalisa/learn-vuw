<template>
  <assignments/>
</template>

<script setup>
import Assignments from "./views/AssignmentsMain.vue";
import { onMounted} from 'vue';

onMounted( () => {
        setTimeout(() => {
            document.title = 'Episode 143: Lifecycle Hooks, Fake APIs, and AJAX';
        }, 1000);
    });

</script>

<style scoped>

</style>