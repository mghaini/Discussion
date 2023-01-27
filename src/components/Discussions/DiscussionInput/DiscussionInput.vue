<script setup lang="ts">
import { toRefs, ref } from 'vue';

interface Props {
    avatarUrl?: string,
    placeholder?: string
}

const props = withDefaults(defineProps<Props>(), {
    avatarUrl: 'https://www.godaddy.com/garage/wp-content/uploads/judith-kallos-BW-NEW-150x150.jpg'
})
const { avatarUrl } = toRefs(props);

const inputValue = ref<string>('')

const submitComment = () => {
    console.log(inputValue.value);
    inputValue.value = '';
}
</script>

<template>
    <div class="discussion-input">
        <img class="discussion-input__avatar" :src="avatarUrl" alt="avatar">
        <input class="discussion-input__input" type="text" :placeholder="placeholder" v-model="inputValue" @keypress.enter="submitComment">
    </div>
</template>

<style scoped lang="scss">
    .discussion-input {
        display: flex;
        justify-content: space-between;
        align-items: center;
        column-gap: 1.5rem;
        width: 100%;
        margin: 0.75rem auto;

        &__avatar {
            max-width: 3rem;
            max-height: 3rem;
            min-width: 3rem;
            min-height: 3rem;
            border-radius: 50%;
        }

        &__input {
            border: 2px solid var(--color-border-primary);
            display: flex;
            flex-grow: 1;
            flex-basis: auto;
            padding: 0.8rem;
            border-radius: 0.4rem;
            font-size: 1rem;
            background-color: var(--color-background-primary);
            outline: none;
            &::placeholder { 
                color: var(--color-text-mute);
            }
        }
    }
</style>
