<template>
    <div class="relative inline-block">
      <div class="selected-font cursor-pointer flex items-center font-bold text-lg leading-6 mr-6" @click="toggleFontList">
        <span class="mr-2">{{ selectedFont }}</span>
        <i :class="arrowIcon"></i>
      </div>
      <ul v-show="showFontList" class="font-list absolute left-0 p-0 m-0 h-40 w-48 flex flex-col justify-between bg-white">
        <li v-for="font in fontOptions" :key="font" @click="selectFont(font)" class="py-1 px-2 cursor-pointer hover:bg-gray-200 flex items-center pl-6 font-bold text-lg leading-6">
          {{ font }}
        </li>
      </ul>
    </div>
  </template>
  
  <script>
  export default {
  data() {
    return {
      fontOptions: ["sans", "serif", "monospace"],
      selectedFont: "sans",
      showFontList: false,
    };
  },
  mounted() {
    const savedFont = localStorage.getItem("choosedFont");
    if (savedFont) {
      this.selectedFont = savedFont;
      this.applyFont(savedFont);
    }
    window.addEventListener("click", this.handleOutsideClick);
  },
  computed: {
      arrowIcon() {
        return this.showFontList ? "bi-arrow-up" : "bi-arrow-down";
      },
    },
  beforeUnmount() {
    window.removeEventListener("click", this.handleOutsideClick);
  },
  methods: {
    toggleFontList() {
      this.showFontList = !this.showFontList;
    },
    selectFont(font) {
      this.selectedFont = font;
      this.showFontList = false;
      this.applyFont(font);
      localStorage.setItem("choosedFont", font);
    },
    applyFont(font) {
      document.body.style.fontFamily = font;
    },
    handleOutsideClick(event) {
      const fontSelector = this.$el;
      if (!fontSelector.contains(event.target)) {
        this.showFontList = false;
      }
    },
  },
};
  </script>  