<script setup lang="ts">
import { ref, computed } from 'vue';
import AuroraBackground from './components/AuroraBackground.vue';
import ShinyText from './components/ShinyText.vue';

const currentLang = ref<'ru' | 'en'>('en');

const t = {
  ru: {
    aboutHeader: "О МОЁМ ПУТИ",
    stackHeader: "АРСЕНАЛ",
    projectsHeader: "ПРОЕКТЫ",
    bio: "Специализируюсь на создании масштабируемых веб-приложений с использованием Vue 3 и TypeScript. Мой подход базируется на архитектуре FSD. Опыт 1.5+ года. Участвовал в разработке трейдинг-ботов и систем управления активами.",
    nav: ["Home", "About", "Stack", "Work"],
    footer: "Адски хороший код — 2025"
  },
  en: {
    aboutHeader: "ABOUT MY PATH",
    stackHeader: "TECH ARSENAL",
    projectsHeader: "FEATURED WORK",
    bio: "Specializing in building scalable web applications with Vue 3 and TypeScript. My approach is based on FSD architecture. 1.5+ years of experience. Participated in the development of trading bots and complex systems.",
    nav: ["Home", "About", "Stack", "Work"],
    footer: "Devilishly good code — 2025"
  }
};

const content = computed(() => t[currentLang.value]);

// Исправлено: жестко типизируем массив ID
const sectionIds: string[] = ['home', 'about', 'stack', 'projects'];

const scrollTo = (id: string) => {
  const element = document.getElementById(id);
  if (element) {
    element.scrollIntoView({ behavior: 'smooth' });
  }
};

const arsenal = [
  { name: 'Vue.js', img: 'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/vuejs/vuejs-original.svg' },
  { name: 'TypeScript', img: 'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/typescript/typescript-original.svg' },
  { name: 'Tailwind', img: 'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/tailwindcss/tailwindcss-original.svg' },
  { name: 'Node.js', img: 'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/nodejs/nodejs-original.svg' },
  { name: 'Go', img: 'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/go/go-original-wordmark.svg' },
  { name: 'Docker', img: 'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/docker/docker-original.svg' },
  { name: 'Postgres', img: 'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/postgresql/postgresql-original.svg' },
  { name: 'Figma', img: 'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/figma/figma-original.svg' },
];

const projects = [
  { title: "Trading Bot", desc: "Lead Frontend Developer for Telegram Mini App.", link: "https://github.com/GodSpeedsT/telegram-trading-mini-app.git", tags: ["Vue 3", "TS"] },
  { title: "FSD Core", desc: "Modular asset management system.", link: "#", tags: ["FSD", "TS"] },
  { title: "Eco Tracker", desc: "Deployment and monitoring system on Go.", link: "#", tags: ["Go", "Docker"] },
  { title: "Magma UI", desc: "Modern portfolio with custom shaders.", link: "#", tags: ["GSAP", "OGL"] },
];
</script>

<template>
  <div class="h-screen overflow-y-scroll snap-y snap-mandatory bg-[#050505] text-white scroll-smooth relative">

    <div class="fixed inset-0 pointer-events-none z-[1] overflow-hidden">
      <div class="absolute top-1/2 left-1/2 -translate-x-1/2 -translate-y-1/2 w-full h-full bg-[radial-gradient(circle,rgba(60,0,0,0.15)_0%,transparent_70%)] animate-pulse-slow"></div>
      <div v-for="n in 8" :key="n" class="lava-drop"
           :style="{
             left: (n * 12) + '%',
             animationDelay: (n * 1.5) + 's',
             animationDuration: (10 + n * 2) + 's',
             background: n % 2 === 0 ? 'radial-gradient(circle, #7f1d1d 0%, transparent 70%)' : 'radial-gradient(circle, #450a0a 0%, transparent 70%)',
             width: (100 + n * 40) + 'px',
             height: (100 + n * 40) + 'px'
           }"></div>
    </div>

    <header class="fixed top-6 left-1/2 -translate-x-1/2 z-[100] flex items-center justify-center pointer-events-none">
      <div class="flex items-center gap-x-3 md:gap-x-6 px-5 md:px-8 py-3 bg-zinc-900/90 border border-white/10 rounded-full shadow-2xl backdrop-blur-md pointer-events-auto">
        <nav class="flex gap-x-3 md:gap-x-6">
          <button v-for="(item, i) in content.nav" :key="item"
                  @click="scrollTo(sectionIds[i] || 'home')"
                  class="text-[10px] md:text-xs font-black text-gray-500 hover:text-white uppercase transition-all">
            {{ item }}
          </button>
        </nav>
        <div class="w-[1px] h-4 bg-white/10" />
        <button @click="currentLang = currentLang === 'ru' ? 'en' : 'ru'"
                class="text-[10px] md:text-xs font-black text-red-600 hover:text-white uppercase px-1">
          {{ currentLang === 'ru' ? 'EN' : 'RU' }}
        </button>
      </div>
    </header>

    <section id="home" class="min-h-screen w-full snap-start flex flex-col items-center justify-center relative overflow-hidden p-6">
      <AuroraBackground />
      <Transition name="language-fade" mode="out-in">
        <div :key="currentLang" class="z-10 flex flex-col items-center gap-y-4 text-center">
          <h1 class="text-3xl sm:text-6xl md:text-8xl lg:text-[110px] font-black tracking-tighter uppercase text-white leading-tight">
            <ShinyText :text="currentLang === 'ru' ? 'ИВАН ОСТРОВСКИЙ' : 'IVAN OSTROVSKY'" :speed="4" />
          </h1>
          <p class="text-red-700 font-mono text-[10px] md:text-sm tracking-[1.2em] uppercase animate-pulse">Front-end developer</p>
        </div>
      </Transition>
    </section>

    <section id="about" class="min-h-screen w-full snap-start flex items-center justify-center p-6 md:p-12 lg:p-24 bg-[#08080a] z-10 relative overflow-hidden">
      <div class="max-w-7xl w-full grid grid-cols-1 lg:grid-cols-[1fr_380px] gap-y-12 items-center">
        <Transition name="language-fade" mode="out-in">
          <div :key="currentLang" class="flex flex-col gap-y-8">
            <h2 class="text-4xl md:text-6xl lg:text-8xl font-black text-white italic tracking-tighter uppercase underline decoration-red-900 underline-offset-[10px]">
              {{ content.aboutHeader }}
            </h2>
            <p class="text-lg md:text-2xl lg:text-4xl text-gray-300 font-light leading-relaxed">
              {{ content.bio }}
            </p>
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

    <section id="stack" class="min-h-screen w-full snap-start flex flex-col items-center justify-center p-6 md:p-12 bg-[#050505] z-10 relative">
      <div class="flex flex-col gap-y-12 w-full max-w-7xl">
        <Transition name="language-fade" mode="out-in">
          <h2 :key="currentLang" class="text-3xl md:text-5xl lg:text-7xl font-black text-white opacity-10 tracking-[0.3em] uppercase text-center">
            {{ content.stackHeader }}
          </h2>
        </Transition>
        <div class="grid grid-cols-2 sm:grid-cols-3 md:grid-cols-4 lg:grid-cols-6 xl:grid-cols-8 gap-4 md:gap-8">
          <div v-for="skill in arsenal" :key="skill.name"
               class="group bg-zinc-900/50 border border-white/5 rounded-[24px] p-6 md:p-10 flex flex-col items-center gap-y-4 hover:bg-zinc-800 hover:border-red-600/50 transition-all duration-500">
            <img :src="skill.img" class="w-12 h-12 md:w-20 md:h-20 group-hover:scale-110 transition-all duration-500" :alt="skill.name">
            <span class="text-[8px] md:text-[10px] font-bold tracking-widest text-white opacity-40 group-hover:opacity-100 uppercase text-center">{{ skill.name }}</span>
          </div>
        </div>
      </div>
    </section>

    <section id="projects" class="min-h-screen w-full snap-start flex flex-col items-center justify-center p-8 md:p-12 bg-[#08080a] z-10 relative">
      <div class="flex flex-col gap-y-12 w-full max-w-7xl">
        <Transition name="language-fade" mode="out-in">
          <h2 :key="currentLang" class="text-3xl md:text-5xl lg:text-7xl font-black text-white opacity-10 tracking-[0.2em] uppercase text-center">
            {{ content.projectsHeader }}
          </h2>
        </Transition>
        <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
          <a v-for="p in projects" :key="p.title" :href="p.link" target="_blank"
             class="group bg-zinc-900/40 border border-white/5 p-8 rounded-[32px] hover:border-red-600/50 transition-all duration-500 relative overflow-hidden flex flex-col gap-y-6">
            <div class="flex flex-col gap-y-4 relative z-10">
              <h3 class="text-xl md:text-4xl font-bold text-white uppercase group-hover:text-red-500 transition-colors tracking-tight">{{ p.title }}</h3>
              <p class="text-gray-400 text-sm md:text-xl font-light">{{ p.desc }}</p>
              <div class="flex flex-wrap gap-3">
                <span v-for="t in p.tags" :key="t" class="px-4 py-1.5 bg-white/5 border border-white/10 text-[9px] font-mono text-red-500 rounded-full font-black uppercase">#{{ t }}</span>
              </div>
            </div>
          </a>
        </div>
      </div>
    </section>

    <footer class="w-full text-center z-10 p-12 bg-[#08080a]">
      <p class="text-white/5 font-mono text-[9px] tracking-[1em] uppercase">{{ content.footer }}</p>
    </footer>

    <div class="fixed inset-0 pointer-events-none z-[5] opacity-[0.03] bg-[url('https://grainy-gradients.vercel.app/noise.svg')]" />
  </div>
</template>

<style>
body { margin: 0; background: #050505; -webkit-font-smoothing: antialiased; }
::-webkit-scrollbar { display: none; }
.snap-start { scroll-snap-align: start; scroll-snap-stop: always; }

.language-fade-enter-active, .language-fade-leave-active { transition: all 0.5s ease; }
.language-fade-enter-from { opacity: 0; filter: blur(10px); transform: translateY(5px); }
.language-fade-leave-to { opacity: 0; filter: blur(10px); transform: translateY(-5px); }

.lava-drop { position: absolute; bottom: -250px; border-radius: 50%; filter: blur(60px); animation: float-lava linear infinite; opacity: 0; }
@keyframes float-lava {
  0% { transform: translateY(0); opacity: 0; }
  15% { opacity: 0.4; }
  50% { transform: translateY(-60vh) scale(1.3); opacity: 0.2; }
  100% { transform: translateY(-130vh); opacity: 0; }
}
@keyframes pulse-slow { 0%, 100% { transform: scale(1) translate(-50%, -50%); } 50% { transform: scale(1.1) translate(-50%, -50%); } }
.card-float-wrapper { animation: float-card 8s ease-in-out infinite; }
@keyframes float-card { 0%, 100% { transform: translateY(0); } 50% { transform: translateY(-20px); } }
* { margin: 0; transition-timing-function: cubic-bezier(0.4, 0, 0.2, 1); }
</style>
