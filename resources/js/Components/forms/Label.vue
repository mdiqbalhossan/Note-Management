<script setup>
defineProps(["value", "id", "customClass", "req"]);
</script>

<template>
    <label
        :for="id"
        class="mb-2 mr-1 text-sm font-medium text-gray-900 dark:text-white"
        :class="customClass"
    >
        <span v-if="value">{{ value }}</span>
        <span v-else><slot /></span>
    </label>
    <span class="text-red-600 font-bold" v-if="req">*</span>
</template>
