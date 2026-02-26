<script setup lang="ts">
import { ref, onMounted } from 'vue';
import gsap from 'gsap';

const props = defineProps({
  text: {
    type: String,
    required: true
  },
  delay: {
    type: Number,
    default: 150 // задержка между словами в мс
  },
  animateBy: {
    type: String,
    default: 'words' // можно выбрать 'words' (слова) или 'letters' (буквы)
  },
  className: {
    type: String,
    default: ''
  }
});

const root = ref<HTMLElement | null>(null);

onMounted(() => {
  if (!root.value) return;

  // Находим все элементы для анимации (слова или буквы)
  const elements = root.value.querySelectorAll('.blur-item');

  // Настраиваем наблюдатель появления на экране
  const observer = new IntersectionObserver((entries) => {
    entries.forEach((entry) => {
      if (entry.isIntersecting) {
        // Запускаем GSAP анимацию
        gsap.fromTo(elements,
          {
            filter: 'blur(10px)',
            opacity: 0,
            y: 20
          },
          {
            filter: 'blur(0px)',
            opacity: 1,
            y: 0,
            stagger: props.delay / 1000,
            duration: 1.2,
            ease: 'power3.out',
          }
        );
        // Отключаем наблюдение после того, как анимация один раз сработала
        observer.unobserve(entry.target);
      }
    });
  }, { threshold: 0.1 });

  observer.observe(root.value);
});
</script>

<template>
  <div ref="root" :class="['flex flex-wrap gap-x-[0.3em] leading-tight', className]">
    <span
      v-for="(item, index) in (animateBy === 'words' ? text.split(' ') : text.split(''))"
      :key="index"
      class="blur-item inline-block will-change-[transform,filter,opacity]"
    >
      <!-- Если это пробел в режиме букв, заменяем на неразрывный пробел -->
      {{ item === ' ' ? '\u00A0' : item }}
    </span>
  </div>
</template>

<style scoped>
/* Дополнительные стили не требуются, так как всё на Tailwind и GSAP */
</style>
