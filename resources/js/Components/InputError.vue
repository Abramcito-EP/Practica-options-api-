<template>
    <div v-show="message">
        <p class="text-sm text-red-600">
            {{ message }}
        </p>
    </div>
</template>

<script>
export default {
    name: 'InputError',
    props: {
        message: {
            type: String,
        },
    },
};
</script>