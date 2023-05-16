<template>
  <div>
    <div v-if="error" v-html="error"></div>
    <div v-else>
      <div v-if="results && results.length > 0">
        <div v-for="(entry, index) in results" :key="index" class="mt-12 pb-32">
          <div class="flex justify-between">
            <div class="result-main_text">
              <h2 class="word font-bold text-6xl">{{ entry.word }}</h2>
              <span class="phonetic font-normal text-2xl leading-7 mt-3">{{ entry.phonetic }}</span>
            </div>
            <button class="play-phonetic w-20 h-20 cursor-pointer" @click="playPhonetic(entry.phonetics)"><i class="bi bi-play-fill"></i></button>
          </div>
          <div v-for="(meaning, index) in entry.meanings" :key="index">
            <span class="meaning-name flex font-bold text-2xl leading-6 mt-10">{{ meaning.partOfSpeech }} <span class="mt-3 w-full h-px bg-gray-300 ml-8 rounded"></span> </span>
            <span class="meaning block font-normal text-xl leading-5">Meaning</span>
            <div v-for="(definition, index) in meaning.definitions" :key="index">
              <ul class="definition-list" v-if="definition.definition">
                <li>{{ definition.definition }}</li>
              </ul>
              <ul v-if="definition.example">
                <li class="definition-example not-italic font-normal text-lg leading-6">{{ definition.example }}</li>
              </ul>
            </div>
            <div v-if="meaning.synonyms && meaning.synonyms.length > 0" class="synonyms font-bold text-xl leading-5 mt-10"><span class="font-normal text-xl leading-5 mr-10">Synonyms</span> {{ meaning.synonyms[0] }}</div>
          </div>

        <span class="full-line block w-full h-px bg-gray-300"></span>
        <div class="source font-normal text-sm leading-4">source: <a :href="entry.sourceUrls[0]" class="ml-6 no-underline" target="_blank">{{ entry.sourceUrls[0] }} <i class="bi bi-box-arrow-up-right
"></i></a></div>
        </div>
      </div>
      <div v-else class="no-result flex flex-col text-center">
        <span class="text-6xl mb-10">😕</span>
        <h3 class="font-bold text-xl leading-6 mb-6">No Definitions Found</h3>
        <p class="font-normal text-lg leading-6">Sorry pal, we couldn't find definitions for the word you were looking for. You can try the search again at later time or head to the web instead.</p></div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    results: {
      type: Array,
      default: null
    }
  },
  data() {
    return {
      isLoading: false,
      error: null
    };
  },
  methods: {
    playPhonetic(phonetics) {
      const audio = new Audio();
      const audioSource = phonetics.find(phonetic => phonetic.audio);
      if (audioSource) {
        audio.src = audioSource.audio;
        audio.play();
      }
    }
  },
  watch: {
    results: {
      immediate: true,
      handler(newResults) {
        if (newResults) {
          this.isLoading = false;
          this.error = null;
        } else {
          this.isLoading = false;
          this.error = '<p>No results found. Please try a different search term.</p>';
        }
      }
    }
  }
};
</script>
