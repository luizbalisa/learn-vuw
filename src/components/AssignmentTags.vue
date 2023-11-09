<template>
    <div class="flex gap-2">
        <!--user clicks on a tag, we then emit a change with that tag that was clicked-->
        <!--note that both class (class and :class) properties will be merged-->
        <!--update:modelValue is by convention and has to be named like that-->
        <button @click="$emit('update:currentTag', tag)" v-for="tag in tags" class="border rounded px-1 py-px text-xs"
            :class="{ 'border-blue-500 text-blue-500': tag === currentTag }">
            {{ tag }}
        </button>
    </div>
</template>

<script setup>
import { computed, defineProps } from 'vue';
const props = defineProps({
    dataTags: Array,
    // v-model="currentTag" from AssignmentList
    currentTag: String // vue specific variable for v-model bindings, v-model="currentTag" 2 way binds to this
});

const tags = computed(() => {
    // Set returns a unique list
    return ['all', ...new Set(props.dataTags)];

});
</script>

<style lang="scss" scoped></style>