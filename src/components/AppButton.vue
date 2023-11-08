<template>
      <button
          :class="{
                'border rounded px-5 py-2 disabled:cursor-not-allowed': true,
                'bg-blue-600 hover:bg-blue-700': props.type === 'primary',
                'bg-purple-200 hover:bg-purple-400':props.type === 'secondary',
                'bg-gray-200 hover:bg-gray-400': props.type === 'muted',
                'is-loading': props.processing
            }"
          :disabled="props.processing"
      >
        <slot/>
      </button>
</template>

<script setup>
import { defineProps } from 'vue';
const props = defineProps({
    type: { // name of property
            type: String, // type for property
            default: 'primary'
        },

        processing: {
            type: Boolean,
            default: false
        }  
})

</script>

<style lang="scss" scoped>

</style>