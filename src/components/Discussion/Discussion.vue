<script setup lang="ts">
import useDiscussion from './scripts/useDiscussion';

const { discussionData } = useDiscussion();
</script>

<template>
    <div>
        {{ discussionData }}
    </div>
</template>

<style scoped lang="scss">
    
</style>
