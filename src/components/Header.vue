<script>
import Icon from '@/assets/logo.svg'
import ChooseFont from './ChooseFont.vue';
import ThemeToggler from './ThemeToggler.vue';
export default {
    computed: {
        iconUrl() {
            return Icon;
        }
    },
    components: { ChooseFont, ThemeToggler }
}
</script>
<template>
  <header class="flex justify-between">
    <a href="#" class="logo">
      <img :src="iconUrl" alt="logo">
    </a>
    
     <div class="right">
      <ChooseFont />
      <ThemeToggler> </ThemeToggler>
    </div>
  </header>
</template> 