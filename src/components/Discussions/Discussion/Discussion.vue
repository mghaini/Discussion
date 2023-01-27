<script setup lang="ts">
import { toRefs } from 'vue';
import DiscussionComment from '../DiscussionComment/DiscussionComment.vue';
import DiscussionInput from '../DiscussionInput/DiscussionInput.vue';

interface Props {
    discussion: Object
}

const props = defineProps<Props>();
const { discussion } = toRefs(props);


</script>

<template>
    <div class="discussion">
        <div class="divider"></div>
        <div class="discussion__root">
            <DiscussionComment :comment="discussion" :isReply="false" />
        </div>
        <div class="discussion__replies" v-if="discussion.replies.length">
            <DiscussionComment v-for="replyComment in discussion.replies" :comment="replyComment" :isReply="true" />
        </div>
        <div class="discussion__input">
            <DiscussionInput placeholder="Reply" />
        </div>
    </div>
</template>

<style scoped lang="scss">
.discussion {
    .divider {
        display: block;
        margin: auto;
        background-color: var(--color-border-primary);
        width: 100%;
        height: 2px;
        margin-bottom: 2rem;
    }

    &__root {
        padding: 0 1.25rem;
    }

    &__replies {
        padding: 0 1.25rem 0 5.75rem;
    }

    &__input {
        padding: 1.5rem 1.25rem 0 5.75rem;
        width: 100%;
    }
}
</style>
