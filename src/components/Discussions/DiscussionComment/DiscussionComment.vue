<script setup lang="ts">
import { onMounted, toRefs, ref } from 'vue';
import like from '@/components/icons/like.vue';

interface Props {
    comment: object,
    isReply: boolean
}

const props = defineProps<Props>();
const { comment, isReply } = toRefs(props);

const convertTimestampToRelativeDate = (timestamp : number) => {
    const relativeFormat = new Intl.RelativeTimeFormat('en', {
        numeric: 'auto',
    });
    const oneDayInMs = 1000 * 60 * 60 * 24;
    const daysDifference = Math.round(
        (timestamp - new Date().getTime()) / oneDayInMs,
    );

    return relativeFormat.format(daysDifference, 'day');
}

const toggleShowReplyInput = () => {
    
}

const relativeDateRef = ref<string>('');

onMounted(() => {
    relativeDateRef.value = convertTimestampToRelativeDate(comment.value?.date);
})
</script>

<template>
    <div class="discussion-comment" :class="{ 'reply-comment' : isReply }">
        <div class="discussion-comment__avatar">
            <img class="discussion-comment__avatar-image" v-if="comment.user.avatar" :src="comment.user.avatar" alt="avatar">
            <div class="discussion-comment__avatar-char" v-else>
                <span>
                    {{ comment.user.name.substring(0, 1) }}
                </span>
            </div>
            <div class="discussion-comment__avatar-line" v-if="!isReply && comment.replies?.length"></div>
        </div>
        <div class="discussion-comment__content">
            <div class="discussion-comment__content__header">
                <div class="discussion-comment__content__header-name">{{ comment.user.name }}</div>
                <div class="discussion-comment__content__header-date">{{ relativeDateRef }}</div>
            </div>
            <div class="discussion-comment__content__body">
            {{ comment.text }}
            </div>
            <div class="discussion-comment__content__actions">
                <button class="discussion-comment__content__actions-like" :class="{ 'active': comment.iLikedIt }">
                    <like class="like-svg" />
                    <span>{{ comment.likes }}</span>
                </button>
                <button class="discussion-comment__content__actions-reply" v-if="!isReply">Reply</button>
            </div>
        </div>
    </div>
</template>

<style scoped lang="scss">
.discussion-comment {
        display: flex;
        column-gap: 1.5rem;
        margin: 1.5rem 0.5rem auto;

        &.reply-comment {
        }

        &__avatar {
            display: flex;
            flex-direction: column;
            row-gap: 0.5rem;
            height: 100%;
            &-image {
                max-width: 3rem;
                max-height: 3rem;
                min-width: 3rem;
                min-height: 3rem;
                border-radius: 50%;
            }

            &-char {
                max-width: 3rem;
                max-height: 3rem;
                min-width: 3rem;
                min-height: 3rem;
                border-radius: 50%;
                background-color: var(--color-secondary);
                span {
                    color: var(--color-primary);
                    display: block;
                    text-align: center;
                    margin-top: 0.5rem;
                    font-size: 1rem;
                    font-weight: bold;
                }
            }
        }

        &__content {
            &__header {
                display: flex;
                column-gap: 1rem;
                &-name {
                    font-size: 1rem;
                    font-weight: bold;
                    color: var(--color-text-primary);
                }
                &-date {
                    color: var(--color-text-mute);
                }
            }

            &__body {
                padding: 0.5rem 0;
                color: var(--color-text-secondary);
            }

            &__actions {
                display: flex;
                column-gap: 1rem;
                &-like {
                    display: flex;
                    align-items: center;
                    column-gap: 0.75rem;
                    border: none;
                    border-radius: 1rem;
                    padding: 0.5rem 1rem;
                    cursor: pointer;
                    color: var(--color-text-primary);
                    background-color: var(--color-background-secondary);

                    span {
                        display: block;
                    }
                    &.active {
                        background-color: var(--color-primary);
                        color: white;
                        .like-svg {
                            fill: white;
                        }
                    }

                    .like-svg {
                        width: 1rem;
                        fill: var(--color-text-primary);
                    }
                }
                &-reply {
                    color: var(--color-primary);
                    font-size: 1rem;
                    font-weight: bold;
                    border: none;
                    background-color: transparent;
                    cursor: pointer;
                }
            }
        }
    }
</style>
