<template>
  <form action="#" class="flex relative" @submit="handleSubmit">
    <input type="search" name="search" id="search" class="w-full h-16 not-italic font-bold text-xl" placeholder="Search for any word…" v-model="searchTerm" required>
    <button type="submit" class="search-btn absolute w-8 h-8 bg-transparent cursor-pointer" value="search"><i class="bi bi-search w-8 text-xl h-8 block"></i></button>
  </form>
</template>

<script>
export default {
  data() {
    return {
      searchTerm: ''
    };
  },
  methods: {
    handleSubmit(event) {
      event.preventDefault();
      this.fetchData();
      this.updateURL();
    },
    async fetchData() {
      try {
        const response = await fetch(`https://api.dictionaryapi.dev/api/v2/entries/en/${this.searchTerm}`);
        const data = await response.json();
        console.log(data);
        this.$emit('search-complete', data);
      } catch (error) {
        console.error(error);
      }
    },
    updateURL() {
      const url = new URL(window.location.href);
      url.searchParams.set('word', this.searchTerm);
      window.history.pushState({path: url.href}, '', url.href);
    }
  },
  mounted() {
    const urlParams = new URLSearchParams(window.location.search);
    const searchTerm = urlParams.get('word');
    if (searchTerm) {
      this.searchTerm = searchTerm;
      this.fetchData();
    }
  }
};
</script>
