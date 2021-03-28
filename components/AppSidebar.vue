
<script setup>
import { storeToRefs } from 'pinia';
import { useAppStore } from '~/stores/app';
import BingIcon from '~/components/Icons/BingIcon.vue';
import GPTIcon from '~/components/Icons/GPTIcon.vue';

const appStore = useAppStore();
const {
    isMobileMenu,
    isMenuOpen,
    isMenuOpening,
    isMenuClosing,
} = storeToRefs(appStore);

const conversationsStore = useConversationsStore();
const {
    currentConversationId,
    conversations,
    processingController,
} = storeToRefs(conversationsStore);
const {
    startNewConversation,
    setCurrentConversationId,
    deleteConversation,
    clearConversations,
} = conversationsStore;

// sort conversations by updatedAt timestamp
const sortedConversations = computed(() => Object.values(conversations.value).sort((a, b) => b.updatedAt - a.updatedAt));

const isConfirmingClear = ref(false);

const startNewConversationHandler = () => {
    startNewConversation();
    if (isMobileMenu.value) {
        isMenuOpen.value = false;
    }
};

const setCurrentConversationIdHandler = (conversationId) => {
    setCurrentConversationId(conversationId);
    if (isMobileMenu.value) {
        isMenuOpen.value = false;
    }
};

const deleteConversationHandler = (conversationId) => {
    deleteConversation(conversationId);
};

const clearConversationsHandler = () => {
    if (!isConfirmingClear.value) {
        isConfirmingClear.value = setTimeout(() => {
            isConfirmingClear.value = false;
        }, 3000);
        return;
    }
    clearConversations();
    clearTimeout(isConfirmingClear.value);
    isConfirmingClear.value = false;
};
</script>

<template>
    <div
        class="
            flex flex-col bg-purple-300/10 flex-1 max-w-xs shadow-lg
            absolute top-0 left-0 h-screen z-50 w-full
            backdrop-blur-lg
            transition-all duration-300 ease-in-out
        "
        :class="{
            'translate-x-0 absolute lg:static': isMenuOpen,
            '!absolute': isMenuOpening,
            '-translate-x-full': !isMenuOpen,
        }"
    >
        <!-- close button -->
        <Transition name="fade">
            <div
                v-if="isMenuOpen || isMenuClosing"
                class="absolute top-0 -right-8 bottom-0 flex items-center lg:hidden"
            >
                <button
                    @click="isMenuOpen = false"
                    class="
                    bg-purple-300/10 rounded-r backdrop-blur-lg
                    text-white/50 hover:text-white/80
                    focus:outline-none z-10
                    transition duration-300 ease-in-out
                "
                >
                    <Icon name="bx:bx-chevron-left" class="w-8 h-8"/>
                </button>
            </div>
        </Transition>
        <!-- Chat threads -->
        <div class="p-3 pb-0">
            <!-- New Chat -->
            <button
                @click="startNewConversationHandler"
                class="
                    flex flex-row items-center w-full bg-white/5 rounded shadow p-3 mb-3
                    transition duration-300 ease-in-out
                    hover:bg-white/10
                "
                :disabled="!!processingController"
                :class="{ 'cursor-not-allowed': !!processingController }"
            >
                    <span class="flex flex-col flex-1 text-left">
                        <span class="text-sm font-bold text-white/80">New Chat</span>
                        <span class="text-xs text-white/60">Click to start a new chat</span>