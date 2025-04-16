<template>
    <div class="sparkle-container">
        <template v-for="sparkle in sparkles" :key="sparkle.id">
            <div class="sparkle" :style="{
                left: `${sparkle.x}px`,
                top: `${sparkle.y}px`,
                '--angle': `${sparkle.angle}deg`,
                '--size': `${sparkle.size}px`,
            }" />
        </template>
    </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue';

const sparkles = ref([]);
let nextId = 0;
let lastMouseX = 0;
let lastMouseY = 0;
let lastMouseTime = 0;

const createSparkle = (x, y, velocity = 0) => {
    const numParticles = Math.min(Math.max(Math.floor(velocity * 0.5), 6), 12);
    const newSparkles = [];
    const duration = Math.max(800 - velocity * 100, 400);
    const distance = Math.min(40 + velocity * 10, 80);

    for (let i = 0; i < numParticles; i++) {
        const angle = (360 / numParticles) * i;
        const size = Math.random() * (3 + velocity * 0.5) + 2;
        newSparkles.push({
            id: nextId++,
            x,
            y,
            angle,
            size,
            duration,
            distance
        });
    }

    sparkles.value.push(...newSparkles);
    setTimeout(() => {
        sparkles.value = sparkles.value.filter(s => !newSparkles.includes(s));
    }, duration);
};

const handleMouseMove = (event) => {
    const currentTime = performance.now();
    const deltaTime = currentTime - lastMouseTime;

    if (deltaTime > 16) { // Limit to ~60fps
        const x = event.clientX;
        const y = event.clientY;
        const deltaX = x - lastMouseX;
        const deltaY = y - lastMouseY;
        const distance = Math.sqrt(deltaX * deltaX + deltaY * deltaY);
        const velocity = distance / deltaTime;

        if (velocity > 0.1) { // Only create sparkles when moving fast enough
            createSparkle(x, y, velocity);
        }

        lastMouseX = x;
        lastMouseY = y;
        lastMouseTime = currentTime;
    }
};

const handleClick = (event) => {
    const x = event.clientX;
    const y = event.clientY;
    createSparkle(x, y, 1);
};

onMounted(() => {
    window.addEventListener('click', handleClick);
    window.addEventListener('mousemove', handleMouseMove);
});

onUnmounted(() => {
    window.removeEventListener('click', handleClick);
    window.removeEventListener('mousemove', handleMouseMove);
});
</script>

<style scoped>
.sparkle-container {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    pointer-events: none;
    z-index: 9999;
}

.sparkle {
    position: absolute;
    width: var(--size);
    height: var(--size);
    background-color: theme('colors.primary.DEFAULT');
    border-radius: 50%;
    transform-origin: center;
    animation: sparkle var(--duration, 1000ms) ease-out forwards;
}

@keyframes sparkle {
    0% {
        opacity: 1;
        transform: rotate(var(--angle)) translateX(0) scale(1);
    }

    100% {
        opacity: 0;
        transform: rotate(var(--angle)) translateX(var(--distance, 50px)) scale(0);
    }
}
</style>