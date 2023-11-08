<template>
    <section class="space-y-6">
        <!--title and assignments are props (properties) on the AssignmentList component-->
        <assignment-list :assignments="filters.inProgress" title="In Progress"></assignment-list>
        <assignment-list :assignments="filters.completed" title="Completed"></assignment-list>

        <!--when the $emit function is fired on the child component, with the name of 'assignmentCreateAction',-->
        <!--fire the parent function called add-->
        <!--assignmentCreateAction is a custom event-->
        <assignment-create @assignmentCreateAction="add"></assignment-create>
    </section>
</template>

<script setup>
import { onBeforeMount, computed, reactive } from "vue";
import AssignmentList from "../components/AssignmentList.vue";
import AssignmentCreate from "../components/AssignmentCreate.vue";
// import Assignment from "../components/AssignmentItem.vue";

let assignments = reactive([]);

onBeforeMount(() => {
    // start json server first: npx json-server data/db.json -p 3001
    fetch('http://localhost:3001/assignments')
        .then(response => response.json())
        .then(assignment => {
            assignments  = assignment;

            console.log(assignments);
        });
});

const filters = computed(() => {
    return {
        inProgress: assignments.filter(assignment => !assignment.complete),
        completed: assignments.filter(assignment => assignment.complete)
    }
});

// assigmentName argument comes from the child component emit vue function from the second argument
// seems that it can be called whatever you want it to be
function add(assigmentName) {

    const addAssignment = { name: assigmentName };

    // some: performs the specified action for each element in an array
    const assignmentExists = assignments.value.some(obj => obj.name === addAssignment.name);

    if (assignmentExists) {
        alert('Assignment ' + assigmentName + ' already exists');
    }

    if (!assignmentExists) {
        assignments.value.push({
            name: assigmentName,
            completed: false,
            id: assignments.value.length + 1,
            tag: 'none'
        });
    }
}
</script>

<style lang="scss" scoped></style>
