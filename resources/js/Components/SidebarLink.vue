<script setup>
import { computed } from 'vue';
import { Link } from '@inertiajs/vue3';

const props = defineProps({
    href: {
        type: String,
        required: true,
    },
    active: {
        type: Boolean,
    },
});

const classes = computed(() =>
    props.active
        ? 'relative px-4 py-3 flex items-center space-x-4 rounded-xl text-white bg-gradient-to-r from-yellow-400 to-red-600'
        : 'px-4 py-3 flex items-center space-x-4 rounded-md text-gray-600 group'
);
</script>

<template>
    <Link :href="href" :class="classes">
        <slot />
    </Link>
</template>
