<template>
    <div class="dark-theme-toggler relative w-16 h-8">
      <input type="checkbox" id="dark-theme-toggle" class="hidden" v-model="isDarkMode">
      <label for="dark-theme-toggle" class="absolute top-0 left-0 w-16 h-8 cursor-pointer"></label>
    </div>
    <i class="bi bi-moon moon mt-1 ml-5 text-lg"></i>
  </template>
  
  <script>
export default {
  data() {
    return {
      isDarkMode: false,
    };
  },
  mounted() {
    this.loadTheme();
  },
  watch: {
    isDarkMode(value) {
      this.saveTheme(value);
      this.applyTheme(value);
    },
  },
  methods: {
    saveTheme(value) {
      localStorage.setItem('theme', value ? 'dark' : 'light');
    },
    loadTheme() {
      const theme = localStorage.getItem('theme');
      this.isDarkMode = theme === 'dark';
      this.applyTheme(this.isDarkMode);
    },
    applyTheme(value) {
      if (value) {
        document.body.classList.add('dark-theme');
      } else {
        document.body.classList.remove('dark-theme');
      }
    },
  },
};
  </script>
  