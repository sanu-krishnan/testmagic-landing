<script setup lang="ts">
import { ref, onMounted, watch } from "vue";

const isDark = ref(false);

const setGridBg = (dark: boolean) => {
    const strokeColor = dark ? "#ffffff" : "#000000";
    const encodedSvg = encodeURIComponent(`
    <svg xmlns="http://www.w3.org/2000/svg" width="48" height="48" viewBox="0 0 48 48" fill="none" stroke="${strokeColor}" opacity="0.15" stroke-width="1">
      <path d="M 48 0 L 0 0 L 0 48"></path>
    </svg>
  `);
    const url = `url("data:image/svg+xml,${encodedSvg}")`;
    document.documentElement.style.setProperty("--grid-bg", url);
};

onMounted(() => {
    const updateTheme = () => {
        const dark = document.documentElement.classList.contains("dark");
        isDark.value = dark;
        setGridBg(dark); // <-- set it immediately on mount
    };

    updateTheme();

    const observer = new MutationObserver(updateTheme);
    observer.observe(document.documentElement, {
        attributes: true,
        attributeFilter: ["class"],
    });
});
</script>



<template>
    <div class="fixed inset-0 w-full h-full bg-background">
        <div class="absolute inset-0 w-full h-full bg-repeat bg-[length:48px_48px]"
            style="background-image: var(--grid-bg)">
            <div class="absolute inset-0 w-full h-full bg-gradient-to-b from-primary/0 to-primary/20">
                <slot />
            </div>
        </div>
    </div>
</template>
