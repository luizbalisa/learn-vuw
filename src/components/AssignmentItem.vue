<template>
  <li>
    <label class="p-2 flex justify-between items-center">
      {{assignment.name }}
      <span class="border rounded px-1 py-px text-xs text-gray-400">{{assignment.tag }}</span>
       <input type="checkbox" v-model="assignment.complete" class="ml-3"> 
    </label>
  </li>
</template>

<script setup>
import { defineProps } from 'vue';
defineProps({
  assignment: Object
}); 
</script>

<style lang="scss" scoped></style>