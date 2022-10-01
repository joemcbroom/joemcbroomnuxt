<script setup>
import '~/assets/css/tailwind.css';

const title = ref('Joe McBroom');
const router = useRouter();

router.beforeEach((to, from, next) => {
  if (to.meta.title) {
    title.value = to.meta.title;
  } else {
    title.value = 'Joe McBroom';
  }
  next();
});

useHead({
  title: computed(() => title.value),
  meta: [
    {
      name: 'viewport',
      content: 'width=device-width, initial-scale=1',
    },
  ],
});

const isDark = useDarkMode();

onMounted(() => {
  const prefersDark =
    localStorage.getItem('theme') === 'dark' ||
    (!('theme' in localStorage) &&
      window.matchMedia('(prefers-color-scheme: dark)').matches);
  isDark.value = prefersDark;
});
</script>
<template>
  <div :class="isDark ? 'dark' : ''">
    <main
      class="min-h-screen bg-sky-100 dark:bg-sky-800 text-sky-800 dark:text-sky-100 text-sm sm:text-lg"
    >
      <NavBar />
      <NuxtPage />
    </main>
  </div>
</template>
