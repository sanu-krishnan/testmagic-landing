<script setup>
import { ref, onMounted } from 'vue';

const theme = ref('light');

onMounted(() => {
    const updateTheme = () => {
        theme.value = document.documentElement.classList.contains('dark') ? 'dark' : 'light';
    };

    updateTheme();

    // Watch for theme changes using MutationObserver
    const observer = new MutationObserver(updateTheme);
    observer.observe(document.documentElement, {
        attributes: true,
        attributeFilter: ['class']
    });
});
</script>

<template>
    <img :src="theme === 'dark' ? 'test-magic-logo-text-dark.svg' : 'testmagic-logo.svg'"
        :alt="theme === 'dark' ? 'TestMagic Dark Logo' : 'TestMagic Logo'" class="h-9" />
</template>