<script setup>
import { Bars3Icon, XCircleIcon } from '@heroicons/vue/24/outline';
import DarkSelector1 from './DarkSelector.vue';
const showNav = ref(false);
const navPages = [
  { name: 'Home', path: '/' },
  { name: 'About', path: '/about' },
  { name: 'Contact', path: '/contact' },
];
</script>

<template>
  <nav
    class="w-full flex flex-wrap gap-4 px-2 py-3 justify-between items-center text-sky-800 dark:text-sky-100 bg-sky-50 dark:bg-sky-900"
  >
    <div class="mr-auto flex items-center gap-1">
      <img src="/img/logo.png" alt="Joe McBroom Logo" class="w-10" />
      <span class="whitespace-nowrap">Joe McBroom</span>
    </div>
    <span class="grid place-items-center sm:hidden" @click="showNav = !showNav">
      <Bars3Icon
        class="w-6 h-6 text-sky-900 dark:text-sky-50 sm:hidden"
        v-show="!showNav"
      />
    </span>
    <div
      class="flex-col sm:flex-row sm:flex gap-4 w-full sm:w-auto justify-center items-center h-screen sm:h-auto absolute sm:relative text-xl sm:text-base top-0 left-0 bg-sky-50 dark:bg-sky-900"
      :class="showNav ? 'flex' : 'hidden'"
    >
      <NuxtLink
        v-for="page in navPages"
        :key="page.name"
        :to="page.path"
        class="hover:text-sky-900 dark:hover:text-sky-50"
        @click="showNav = false"
      >
        {{ page.name }}
      </NuxtLink>
      <DarkSelector />
      <XCircleIcon
        class="w-8 h-8 text-sky-900 dark:text-sky-50 absolute top-6 right-2 sm:hidden"
        v-show="showNav"
        @click="showNav = !showNav"
      />
    </div>
  </nav>
</template>
