<script setup lang="ts">
import { computed, } from "vue";

const gridBg = computed(() => {
    const encodedSvg = encodeURIComponent(`
    <svg xmlns="http://www.w3.org/2000/svg" width="48" height="48" viewBox="0 0 48 48" fill="none" stroke="#000" opacity="0.15" stroke-width="1">
      <path d="M 48 0 L 0 0 L 0 48"></path>
    </svg>
  `);
    return `url("data:image/svg+xml,${encodedSvg}")`;
});
</script>

<template>
    <div class="fixed inset-0 w-full h-full bg-background">
        <div class="absolute inset-0 w-full h-full bg-repeat bg-[length:48px_48px]"
            :style="{ backgroundImage: gridBg }">
            <div class="absolute inset-0 w-full h-full bg-gradient-to-b from-primary/0 to-primary/20">
                <slot />
            </div>
        </div>
    </div>
</template>
