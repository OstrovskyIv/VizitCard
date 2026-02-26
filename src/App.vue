<script setup lang="ts">
import { ref, computed, onMounted, onUnmounted } from 'vue';
import AuroraBackground from './components/AuroraBackground.vue';
import ShinyText from './components/ShinyText.vue';

const currentLang = ref<'ru' | 'en'>('en');
const isHeaderHidden = ref(false);
let hideTimer: ReturnType<typeof setTimeout> | null = null;

const resetTimer = () => {
  isHeaderHidden.value = false;
  if (hideTimer) clearTimeout(hideTimer);

  if (window.innerWidth < 768) {
    hideTimer = setTimeout(() => {
      isHeaderHidden.value = true;
    }, 2000);
  }
};

onMounted(() => {
  resetTimer();
  window.addEventListener('scroll', resetTimer, { passive: true });
  window.addEventListener('touchstart', resetTimer, { passive: true });
});

onUnmounted(() => {
  if (hideTimer) clearTimeout(hideTimer);
  window.removeEventListener('scroll', resetTimer);
  window.removeEventListener('touchstart', resetTimer);
});

const t = {
  ru: {
    aboutHeader: "О МОЁМ ПУТИ", stackHeader: "ТЕХНОЛОГИИ", toolsHeader: "ИНСТРУМЕНТАРИЙ", projectsHeader: "ПРОЕКТЫ",
    bio: "Специализируюсь на создании масштабируемых веб-приложений с использованием Vue 3 и TypeScript. Мой подход базируется на архитектуре FSD. Опыт 1.5+ года. Участвовал в разработке трейдинг-ботов, RP-проектов и e-commerce систем. Владею фронтенд и бэкенд технологиями (Java, Python, Go).",
    nav: ["Home", "About", "Stack", "Work"], footer: "Адски хороший код — 2025",
    projects: [
      { title: "Trading Mini App", desc: "Главный фронтенд-разработчик трейдинг бота. Сложные графики и real-time данные.", tags: ["Vue 3", "Trading", "WebSockets"], link: "https://github.com/GodSpeedsT/telegram-trading-mini-app" },
      { title: "Last Zone RP", desc: "Разработка уникальных интерфейсов для RolePlay проекта в сеттинге выживания.", tags: ["UI/UX", "Game Design"], link: "https://github.com/OstrovskyIv/Last-Zone-RP" },
      { title: "Web Shopping Store", desc: "Интернет-магазин с корзиной и каталогом товаров.", tags: ["E-commerce", "Vue", "State"], link: "https://github.com/OstrovskyIv/web_shopping_store.git" },
      { title: "Travel Map", desc: "Интерактивная карта путешествий для отслеживания маршрутов.", tags: ["Leaflet", "Maps", "TS"], link: "https://github.com/OstrovskyIv/TravelMap.git" }
    ]
  },
  en: {
    aboutHeader: "ABOUT MY PATH", stackHeader: "TECH STACK", toolsHeader: "TOOLS", projectsHeader: "FEATURED WORK",
    bio: "Specializing in building scalable web applications with Vue 3 and TypeScript. My approach is based on FSD architecture. 1.5+ years of experience. Involved in developing trading bots, RP projects, and e-commerce systems. Proficient in both frontend and backend (Java, Python, Go).",
    nav: ["Home", "About", "Stack", "Work"], footer: "Devilishly good code — 2025",
    projects: [
      { title: "Trading Mini App", desc: "Lead Frontend Developer for a trading bot. Complex charts and real-time data.", tags: ["Vue 3", "Trading", "WebSockets"], link: "https://github.com/GodSpeedsT/telegram-trading-mini-app" },
      { title: "Last Zone RP", desc: "Developing unique interfaces for a survival-themed RolePlay project.", tags: ["UI/UX", "Game Design"], link: "https://github.com/OstrovskyIv/Last-Zone-RP" },
      { title: "Web Shopping Store", desc: "Full-featured online store with a shopping cart and product catalog.", tags: ["E-commerce", "Vue", "State"], link: "https://github.com/OstrovskyIv/web_shopping_store.git" },
      { title: "Travel Map", desc: "Interactive travel map for tracking routes and locations.", tags: ["Leaflet", "Maps", "TS"], link: "https://github.com/OstrovskyIv/TravelMap.git" }
    ]
  }
};

const content = computed(() => t[currentLang.value]);
const sectionIds: string[] = ['home', 'about', 'stack', 'projects'];
const scrollTo = (id: string | undefined) => {
  if (id) document.getElementById(id)?.scrollIntoView({ behavior: 'smooth' });
};

const lavaBlobs = Array.from({ length: 8 }).map((_, i) => ({
  id: i,
  left: Math.random() * 100,
  size: 300 + Math.random() * 300,
  duration: 20 + Math.random() * 15,
  delay: Math.random() * -30,
  opacity: 0.04 + Math.random() * 0.04,
  color: i % 2 === 0 ? 'rgba(50, 0, 0, 1)' : 'rgba(30, 0, 0, 1)'
}));

const languages = [
  { name: 'Vue.js', img: 'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/vuejs/vuejs-original.svg', stars: 3 },
  { name: 'TypeScript', img: 'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/typescript/typescript-original.svg', stars: 2 },
  { name: 'Tailwind', img: 'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/tailwindcss/tailwindcss-original.svg', stars: 3 },
  { name: 'HTML5', img: 'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/html5/html5-original.svg', stars: 3 },
  { name: 'CSS3', img: 'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/css3/css3-original.svg', stars: 3 },
  { name: 'JavaScript', img: 'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/javascript/javascript-original.svg', stars: 2 },
  { name: 'Java', img: 'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/java/java-original.svg', stars: 1 },
  { name: 'Python', img: 'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/python/python-original.svg', stars: 1 },
  { name: 'Go', img: 'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/go/go-original-wordmark.svg', stars: 1 },
];

const toolsList = [
  { name: 'WebStorm', img: 'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/webstorm/webstorm-original.svg' },
  { name: 'VS Code', img: 'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/vscode/vscode-original.svg' },
  { name: 'Figma', img: 'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/figma/figma-original.svg' },
  { name: 'Docker', img: 'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/docker/docker-original.svg' },
];
</script>

<template>
  <div class="h-screen overflow-y-scroll snap-y snap-mandatory bg-[#050505] text-white scroll-smooth relative">

    <div class="fixed inset-0 pointer-events-none z-[1] overflow-hidden bg-black">
      <div class="absolute top-1/2 left-1/2 -translate-x-1/2 -translate-y-1/2 w-full h-full bg-[radial-gradient(circle,rgba(40,0,0,0.08)_0%,transparent_85%)] animate-pulse-slow"></div>
      <div v-for="blob in lavaBlobs" :key="blob.id"
           class="lava-blob"
           :style="{
             left: blob.left + '%',
             width: blob.size + 'px',
             height: blob.size + 'px',
             animationDelay: blob.delay + 's',
             animationDuration: blob.duration + 's',
             background: `radial-gradient(circle, ${blob.color} 0%, transparent 70%)`,
             opacity: blob.opacity
           }">
      </div>
    </div>

    <header :class="['fixed top-0 left-1/2 -translate-x-1/2 z-[100] w-full flex flex-col items-center pt-6 transition-all duration-700 pointer-events-none', isHeaderHidden ? '-translate-y-[85%]' : 'translate-y-0']">
      <div class="flex items-center gap-x-3 md:gap-x-6 px-5 md:px-8 py-3 bg-zinc-900/95 border border-white/10 rounded-full shadow-2xl backdrop-blur-md pointer-events-auto">
        <nav class="flex gap-x-3 md:gap-x-6">
          <button v-for="(item, i) in content.nav" :key="item" @click="scrollTo(sectionIds[i])"
                  class="text-[10px] md:text-xs font-black text-gray-500 hover:text-white transition-all active:scale-95 uppercase">{{ item }}</button>
        </nav>
        <div class="w-[1px] h-4 bg-white/10" />
        <button @click="currentLang = currentLang === 'ru' ? 'en' : 'ru'" class="text-[10px] md:text-xs font-black text-red-600 hover:text-white uppercase px-1 transition-colors">{{ currentLang === 'ru' ? 'EN' : 'RU' }}</button>
      </div>
      <button v-if="isHeaderHidden" @click="resetTimer" class="mt-4 w-12 h-1.5 bg-red-600/60 rounded-full animate-pulse shadow-[0_0_15px_rgba(220,38,38,0.6)] pointer-events-auto md:hidden"></button>
    </header>

    <section id="home" class="min-h-screen w-full snap-start flex flex-col items-center justify-center relative overflow-hidden p-6 text-center">
      <AuroraBackground />
      <Transition name="language-fade" mode="out-in">
        <div :key="currentLang" class="z-10 flex flex-col items-center gap-y-4">
          <h1 class="text-3xl sm:text-6xl md:text-8xl lg:text-[110px] font-black tracking-tighter uppercase text-white leading-tight">
            <ShinyText :text="currentLang === 'ru' ? 'ИВАН ОСТРОВСКИЙ' : 'IVAN OSTROVSKY'" :speed="4" />
          </h1>
          <p class="text-red-700 font-mono text-[10px] md:text-sm tracking-[1.2em] uppercase animate-pulse">Front-end developer</p>
        </div>
      </Transition>
    </section>

    <section id="about" class="min-h-screen w-full snap-start flex items-center justify-center p-6 md:p-12 lg:p-24 bg-[#08080a]/40 z-10 relative overflow-hidden">
      <div class="max-w-7xl w-full grid grid-cols-1 lg:grid-cols-[1fr_380px] gap-y-12 lg:gap-x-20 items-center">
        <Transition name="language-fade" mode="out-in">
          <div :key="currentLang" class="flex flex-col gap-y-8 text-center lg:text-left">
            <h2 class="text-4xl md:text-6xl lg:text-8xl font-black text-white italic tracking-tighter uppercase underline decoration-red-900 underline-offset-[10px]">{{ content.aboutHeader }}</h2>
            <p class="text-lg md:text-2xl lg:text-4xl text-gray-300 font-light leading-relaxed">{{ content.bio }}</p>
          </div>
        </Transition>
        <div class="flex justify-center lg:justify-end">
          <div class="card-float-wrapper relative">
            <div class="absolute -inset-6 bg-red-600/10 blur-[60px] rounded-full animate-pulse"></div>
            <div class="relative w-60 h-80 md:w-80 md:h-[480px] bg-zinc-900 border-[10px] border-zinc-800 rounded-[40px] shadow-2xl overflow-hidden group hover:border-red-900/50 transition-all duration-700">
              <img src="/assets/Me.png" alt="Ivan Photo" class="w-full h-full object-cover grayscale brightness-100 group-hover:grayscale-0 group-hover:scale-105 transition-all duration-1000" />
            </div>
          </div>
        </div>
      </div>
    </section>

    <section id="stack" class="min-h-screen w-full snap-start flex flex-col items-center justify-center p-6 md:p-12 bg-[#050505]/40 z-10 relative overflow-y-auto">
      <div class="flex flex-col gap-y-12 md:gap-y-16 w-full max-w-7xl px-4 py-20 text-center">
        <div class="flex flex-col gap-y-12">
          <h2 class="text-2xl md:text-5xl font-black text-white opacity-10 tracking-[0.3em] uppercase">{{ content.stackHeader }}</h2>
          <div class="grid grid-cols-2 sm:grid-cols-3 md:grid-cols-4 lg:grid-cols-5 gap-4 md:gap-6">
            <div v-for="skill in languages" :key="skill.name" class="group relative bg-zinc-900/50 border border-white/5 rounded-[24px] p-6 md:p-8 flex flex-col items-center gap-y-4 hover:bg-zinc-800 hover:border-red-600/50 transition-all duration-500 overflow-hidden">
              <div class="absolute top-2 flex gap-0.5 opacity-0 group-hover:opacity-100 transition-opacity"><span v-for="s in skill.stars" :key="s" class="text-red-600 text-[10px]">★</span></div>
              <img :src="skill.img" class="w-10 h-10 md:w-14 md:h-14 group-hover:scale-110 transition-all" :alt="skill.name">
              <span class="text-[8px] md:text-[10px] font-bold tracking-widest text-white opacity-40 group-hover:opacity-100 uppercase">{{ skill.name }}</span>
            </div>
          </div>
        </div>
        <div class="flex flex-col gap-y-12 border-t border-white/5 pt-12 md:pt-16">
          <h2 class="text-2xl md:text-5xl font-black text-white opacity-10 tracking-[0.3em] uppercase">{{ content.toolsHeader }}</h2>
          <div class="grid grid-cols-2 sm:grid-cols-4 gap-4 md:gap-8 justify-center max-w-4xl mx-auto w-full px-4">
            <div v-for="tool in toolsList" :key="tool.name" class="group relative bg-zinc-900/30 border border-white/5 rounded-[24px] p-6 md:p-8 flex flex-col items-center gap-y-4 hover:bg-zinc-800 hover:border-white/20 transition-all duration-500">
              <img :src="tool.img" class="w-10 h-10 md:w-14 md:h-14 group-hover:rotate-[25deg] transition-transform" :alt="tool.name">
              <span class="text-[8px] md:text-[10px] font-bold tracking-widest text-white opacity-30 group-hover:opacity-100 uppercase">{{ tool.name }}</span>
            </div>
          </div>
        </div>
      </div>
    </section>

    <section id="projects" class="min-h-screen w-full snap-start flex flex-col items-center justify-center p-8 md:p-12 bg-[#08080a]/40 z-10 relative">
      <div class="flex flex-col gap-y-12 md:gap-y-16 w-full max-w-7xl px-4 py-20 text-center">
        <Transition name="language-fade" mode="out-in"><h2 :key="currentLang" class="text-3xl md:text-7xl font-black text-white opacity-10 tracking-[0.2em] uppercase">{{ content.projectsHeader }}</h2></Transition>
        <div class="grid grid-cols-1 md:grid-cols-2 gap-6 md:gap-10">
          <TransitionGroup name="language-fade">
            <a v-for="p in content.projects" :key="p.title + currentLang" :href="p.link" target="_blank" class="group bg-zinc-900/40 border border-white/5 p-8 md:p-12 rounded-[32px] hover:bg-zinc-900 hover:border-red-600/50 transition-all duration-500 relative overflow-hidden flex flex-col gap-y-6">
              <div class="flex flex-col gap-y-4 relative z-10 text-left">
                <h3 class="text-xl md:text-4xl font-bold text-white uppercase group-hover:text-red-500 transition-colors tracking-tight leading-tight">{{ p.title }}</h3>
                <p class="text-gray-400 text-sm md:text-xl font-light leading-relaxed">{{ p.desc }}</p>
                <div class="flex flex-wrap gap-3"><span v-for="t in p.tags" :key="t" class="px-4 py-1.5 bg-white/5 border border-white/10 text-[9px] md:text-xs font-mono text-red-500 rounded-full font-black uppercase">#{{ t }}</span></div>
              </div>
            </a>
          </TransitionGroup>
        </div>
      </div>
    </section>

    <footer class="w-full text-center z-10 p-12 bg-[#08080a]">
      <p class="text-white/5 font-mono text-[9px] tracking-[1em] uppercase">{{ content.footer }}</p>
    </footer>

    <div class="noise-overlay" />
  </div>
</template>

<style>
body { margin: 0; background: #050505; -webkit-font-smoothing: antialiased; -moz-osx-font-smoothing: grayscale; overflow: hidden; }
::-webkit-scrollbar { display: none; }
.snap-start { scroll-snap-align: start; scroll-snap-stop: always; }

.noise-overlay {
  position: fixed; inset: 0; pointer-events: none; z-index: 5; opacity: 0.03;
  background-image: url('https://grainy-gradients.vercel.app/noise.svg');
}

.language-fade-enter-active, .language-fade-leave-active { transition: opacity 0.4s ease, filter 0.4s ease, transform 0.4s ease; }
.language-fade-enter-from { opacity: 0; filter: blur(10px); transform: translateY(5px); }
.language-fade-leave-to { opacity: 0; filter: blur(10px); transform: translateY(-5px); }

.lava-blob { position: absolute; bottom: -350px; border-radius: 50%; animation: lava-float linear infinite; will-change: transform, opacity; }
@keyframes lava-float {
  0% { transform: translateY(0) scale(1) translateX(0); opacity: 0; }
  15% { opacity: 1; }
  50% { transform: translateY(-60vh) scale(1.3) translateX(30px); }
  85% { opacity: 1; }
  100% { transform: translateY(-130vh) scale(0.8) translateX(-20px); opacity: 0; }
}

@keyframes pulse-slow { 0%, 100% { transform: scale(1) translate(-50%, -50%); opacity: 0.4; } 50% { transform: scale(1.05) translate(-50%, -50%); opacity: 0.6; } }
.animate-pulse-slow { animation: pulse-slow 8s ease-in-out infinite; }
.card-float-wrapper { animation: float-card 8s ease-in-out infinite; }
@keyframes float-card { 0%, 100% { transform: translateY(0) rotate(-0.5deg); } 50% { transform: translateY(-20px) rotate(0.5deg); } }
* { margin: 0; transition-timing-function: cubic-bezier(0.4, 0, 0.2, 1); }
</style>