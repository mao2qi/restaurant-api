
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