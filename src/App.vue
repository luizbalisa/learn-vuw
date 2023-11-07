<template>
  <assignments></assignments>
</template>

<script setup>
import Assignments from "./Assignments.js";
mounted() {
        setTimeout(() => {
            document.title = 'Episode 13: Lifecycle Hooks, Fake APIs, and AJAX';
        }, 1000);
    },
</script>

<style lang="scss" scoped>

</style>