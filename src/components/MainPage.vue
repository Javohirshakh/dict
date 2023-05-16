<template>
  <div class="container mx-auto p-4 md:p-8 ">
    <Header />
    <SearchBar @search-complete="handleSearchComplete" />
    <SearchResult v-if="searchResults" :results="searchResults" />
  </div> 
</template>

<script>
import { RouterLink, RouterView } from 'vue-router'
import Header from './Header.vue'
import SearchBar from './SearchBar.vue'
import SearchResult from './SearchResult.vue'


export default {
  components: {
    Header,
    SearchBar,
    SearchResult
  },
  data() {
    return {
      searchResults: null
    };
  },
  methods: {
    handleSearchComplete(data) {
      this.searchResults = data;
    }
  }
};
</script>

