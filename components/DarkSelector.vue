<script setup>
import sunUrl from '/img/sun.svg';
import moonUrl from '/img/moon.svg';
const isDark = useDarkMode();

const setDarkMode = value => {
  isDark.value = value;
  localStorage.setItem('theme', value ? 'dark' : '');
};

let imagePath = computed(() => {
  return isDark.value ? sunUrl : moonUrl;
});

watchEffect(() => {
  useHead({
    htmlAttrs: {
      class: isDark.value ? 'dark' : '',
    },
  });
});
</script>

<template>
  <!-- Wrapper -->
  <div
    class="select-none cursor-pointer w-14 overflow-hidden rounded-full p-1 bg-slate-800 dark:bg-slate-50"
    @click="setDarkMode(!isDark)"
  >
    <!-- Icon -->
    <div
      class="flex w-6 aspect-square rounded-full bg-yellow-500 transition-transform duration-200 ease"
      :class="isDark ? 'translate-x-0' : 'translate-x-full'"
    >
      <img :src="imagePath" />
    </div>
  </div>
</template>
