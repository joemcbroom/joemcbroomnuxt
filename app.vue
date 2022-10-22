<script setup>
import '~/assets/css/tailwind.css';

const title = ref('Joe McBroom');
const router = useRouter();
const route = useRoute();

// router.beforeEach((to, _, next) => {
//   if (to.meta.title) {
//     title.value = to.meta.title;
//   } else {
//     title.value = 'Joe McBroom';
//   }
//   next();
// });

useHead({
  title: computed(() => title.value),
  meta: [
    {
      name: 'viewport',
      content: 'width=device-width, initial-scale=1',
    },
  ],
  link: [{ rel: 'icon', type: 'image/png', href: '/img/favicon-32x32.png' }],
});

const isDark = useDarkMode();

onMounted(() => {
  const prefersDark =
    localStorage.getItem('theme') === 'dark' ||
    (!('theme' in localStorage) &&
      window.matchMedia('(prefers-color-scheme: dark)').matches);
  isDark.value = prefersDark;
});

watchEffect(() => {
  title.value = `${route.meta.title} - Joe McBroom` || 'Joe McBroom';
});
</script>
<template>
  <div class="min-h-screen flex flex-col">
    <NavBar />
    <main
      class="bg-sky-100 dark:bg-sky-800 text-sky-800 dark:text-sky-100 text-sm sm:text-lg flex-grow"
    >
      <NuxtPage />
    </main>
  </div>
</template>
