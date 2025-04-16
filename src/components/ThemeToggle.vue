<script setup>
import { ref, onMounted } from 'vue';
import { Sun, Moon } from 'lucide-vue-next';

const theme = ref('light');

onMounted(() => {
    theme.value = localStorage.getItem('theme') || 'light';
    document.documentElement.classList.toggle('dark', theme.value === 'dark');
});

const toggleTheme = () => {
    console.log('toggleTheme');

    theme.value = theme.value === 'dark' ? 'light' : 'dark';
    localStorage.setItem('theme', theme.value);
    document.documentElement.classList.toggle('dark', theme.value === 'dark');
}
</script>

<template>
    <button @click="toggleTheme" class="p-2 border rounded-md bg-background hover:scale-105 transition-transform">
        <Sun v-if="theme === 'light'" class="w-5 h-5" />
        <Moon v-else class="w-5 h-5" />
    </button>
</template>
