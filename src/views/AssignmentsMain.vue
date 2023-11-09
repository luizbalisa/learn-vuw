<template>
    <section class="space-y-6">
        <!--title and assignments are props (properties) on the AssignmentList component-->
        <assignment-list :assignments="filters.inProgress" title="In Progress"/>
        <div  v-show="showCompleted">
            <assignment-list :assignments="filters.completed" title="Completed" @toggle="showCompleted = !showCompleted" can-toggle/>
        </div>
        <!--when the $emit function is fired on the child component, with the name of 'assignmentCreateAction',-->
        <!--fire the parent function called add-->
        <!--assignmentCreateAction is a custom event-->
        <assignment-create @assignmentCreateAction="add"></assignment-create>
    </section>
</template>

<script setup>
import { onMounted, computed, ref, reactive } from "vue";
import AssignmentList from "../components/AssignmentList.vue";
import AssignmentCreate from "../components/AssignmentCreate.vue";

let assignments = reactive(ref([]));
const showCompleted = ref(true)

onMounted(() => {
    fetch('http://localhost:3001/assignments')
        .then(response => {
            if (!response.ok) {
                throw new Error('Network response was not ok');
            }
            return response.json();
        })
        .then(assignment => {
            assignments.value = assignment;
        })
        .catch(error => {
            console.error('Error fetching assignments:', error);
        });
});

const filters = computed(() => {
    return {
        inProgress: assignments.value.filter(assignment => !assignment.complete),
        completed: assignments.value.filter(assignment => assignment.complete)
    }
});

// assigmentName argument comes from the child component emit vue function from the second argument
// seems that it can be called whatever you want it to be
function add(assigmentName) {
        assignments.value.push({
            name: assigmentName,
            completed: false,
            id: assignments.value.length + 1,
            tag: 'none'
        });
}
</script>

<style lang="scss" scoped></style>
