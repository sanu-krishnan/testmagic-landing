<script setup>
import { ref, onMounted } from 'vue';

const theme = ref('light');
const props = defineProps({
    imageSrc: {
        type: String,
    },
    darkImageSrc: {
        type: String,
    },
    altText: {
        type: String,
    },
    additionalClasses: {
        type: String,
    },
});

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
    <img :src="theme === 'dark' ? props.darkImageSrc : props.imageSrc" :alt="props.altText" class="transition-all"
        :class="props.additionalClasses" />
</template>