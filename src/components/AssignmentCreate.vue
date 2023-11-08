<template>
    <form @submit.prevent="add">
        <div class="border border-gray-600 text-black">
            <input v-model="newAssignment" placeholder="New assignment..." class="p-2" required />
            <button type="submit" class="bg-white p-2 border-l">Add</button>
        </div>
    </form>
</template>

<script setup>
import { ref } from 'vue'
const newAssignment = ref('')

function add() {
    // emit this to the parent component
    // note that the second argument here would be the 'name' argument
    // assignmentCreateAction is a custom event
    // when assignmentCreateAction is emitted by this child component, fire the add event on the parent
    this.$emit('assignmentCreateAction', newAssignment.value)

    // clear the new assignment element
    newAssignment.value = ''
}
</script>

<style lang="scss" scoped></style>
