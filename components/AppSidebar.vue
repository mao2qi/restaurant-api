
<script setup>
import { storeToRefs } from 'pinia';
import { useAppStore } from '~/stores/app';
import BingIcon from '~/components/Icons/BingIcon.vue';
import GPTIcon from '~/components/Icons/GPTIcon.vue';

const appStore = useAppStore();
const {
    isMobileMenu,
    isMenuOpen,