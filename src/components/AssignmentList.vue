<template>
  <AssignmentPanel v-show="assignments.length">
    <h2 class="font-bold mb-2">
      {{ title }}
      <span>({{ assignments.length }})</span>
      <button v-show="canToggle" @click="$emit('toggle')">&times;</button>
    </h2> 

    <!--magic $event variable, contains second argument (tag) from $emit-->
    <!--after user clicks on the tag, it emits a change with the tag selected, in turn, this component waits for that change-->
    <!--we will the store that tag selected as the current tag-->
    <assignment-tags v-model:currentTag="currentTag" :data-tags="assignments.map((a) => a.tag)"
      :current-tag="currentTag" />

    <ul class="border border-gray-600 divide-y divide-gray-600 mt-6"> 
      <assignment v-for="assignment in filteredAssignments" :key="assignment.id" :assignment="assignment" />
    </ul> 
    <slot></slot>
  </AssignmentPanel>
</template>

<script setup>
import { ref, defineProps, computed } from "vue";
import Assignment from "./AssignmentItem.vue";
import AssignmentTags from "./AssignmentTags.vue";
import AssignmentPanel from "../components/AssignmentPanel.vue";

const props = defineProps({
  assignments: Array,
  title: String,
  canToggle: { type: Boolean, default: false },
});

let currentTag = ref('all');

const filteredAssignments = computed(() => {
  if (currentTag.value === 'all') {
    return props.assignments;
  }
  console.log("currentTag",props.assignments);
    return props.assignments.filter(a => a.tag === currentTag.value);
});
</script>

<style lang="scss" scoped></style>
