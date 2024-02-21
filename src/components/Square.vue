<script setup lang="ts">
import { ref } from 'vue';

defineProps<{
    value: String
}>();
</script>

<template>
    <div class="p-4 rounded border w-32 h-32 flex items-center justify-center font-bold text-3xl">
        {{ value }}
    </div>
</template>