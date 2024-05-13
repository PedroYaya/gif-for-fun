<template>
  <div>
    <LightBox v-if="!!current_gif" :gif="current_gif" @close="current_gif = null"/>
    <GifSearch @on-search="onSearch($event)"/>
    <GifList v-if="!!gifs" :gifs="gifs" @set-current-gif="setCurrentGif($event)"/>
  </div>
</template>

<script>
import GifList from './components/GifList.vue';
import GifSearch from './components/GifSearch.vue';
import LightBox from './components/LightBox.vue';

export default {
  name: 'App',
  components: {
    GifList,
    GifSearch,
    LightBox
  },
  data() {
    return {
      gifs: [],
      current_gif: null,
      term: 'default',
      API_KEY: 'pLURtkhVrUXr3KG25Gy5IvzziV5OrZGa'
    }
  },
  computed: {
    get_gifs_url() {
      return `https://api.giphy.com/v1/gifs/search?api_key=${this.API_KEY}&q=${this.term}`;
    }
  },
  async mounted() {
    await this.getGifs();
  },
  methods: {
    async getGifs() {
      const response = await fetch(this.get_gifs_url);
      const data = await response.json(); 
      this.gifs = data.data;
    },
    async onSearch(term) {
      this.term = term;
      await this.getGifs();
    },
    setCurrentGif(ev) {
      this.current_gif = ev;
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
