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
} =