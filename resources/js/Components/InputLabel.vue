<template>
    <label class="block text-sm font-medium text-gray-700">
        <span v-if="value">{{ value }}</span>
        <span v-else><slot /></span>
    </label>
</template>

<script>
export default {
    name: 'InputLabel',
    props: {
        value: {
            type: String,
        },
    },
};
</script>
