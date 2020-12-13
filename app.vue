<script setup>
// eslint-disable-next-line import/no-extraneous-dependencies
import 'fork-corner/dist/fork-corner.css';
import { storeToRefs } from 'pinia';
import initForkCorner from '~/fork-corner';
import AppSidebar from '~/components/AppSidebar.vue';
import { useAppStore } from '~/stores/app';
import { useConversationsStore } from '~/stores/conversations';

const appStore = useAppStore();
const conversationsStore = useConversationsStore();

const {
    isMenuOpen,
    isMenuOpening,
} = storeToRefs(appStore);

const {
    conversationTitle,
} = storeToRefs(conversationsStore);

useHead({
    title: `${conversationTitle.value} - PandoraAI`,
    meta: [
        {
            name: 'viewport',
            content: 'width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no',
        },
    ],
});

onMounted(() => {
    initForkCorner();
});
</script>

<template>
    <a
        href="https://github.com/waylaidwanderer/PandoraAI"
        target="_blank"
        id="fork-corner"
        class="fork-corner fc-size-