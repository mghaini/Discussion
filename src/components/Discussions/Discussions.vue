<script setup lang="ts">
import useDiscussion from './scripts/useDiscussion';
import DiscussionInput from './DiscussionInput/DiscussionInput.vue';
import Discussion from './Discussion/Discussion.vue';

const { discussionData } = useDiscussion();
</script>

<template>
    <div class="discussions">
        <div class="discussions__input-wrapper">
            <DiscussionInput placeholder="Start a discussion"/>
        </div>
        <div class="discussions__comment">
            <Discussion v-for="discussion in discussionData" :discussion="discussion" />
        </div>
    </div>
</template>

<style scoped lang="scss">
    .discussions {
        display: flex;
        flex-direction: column;
        align-items: center;
        margin: auto;
        max-width: 700px;

        &__input-wrapper {
            width: 100%;
            padding: 2rem 1.25rem;
            background-color: var(--color-background-secondary);
        }
    }
</style>
