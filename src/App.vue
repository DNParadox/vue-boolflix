<template>
  <div id="app">
    <myHeader @sendText="query" />
    <MyMain :netflixMovie="this.netflixMovie" />
  </div>
</template>

<script>
import myHeader from './components/myHeader.vue';
import MyMain from './components/myMain.vue';
import axios from 'axios'


export default {
  name: 'App',
  components: {
    myHeader,
    MyMain
  },
  data() {
    return {
      textToSearch: "",
      netflixMovie: [],
      getApi: 'https://api.themoviedb.org/3/search/movie?api_key=e99307154c6dfb0b4750f6603256716d&query=ritorno+al+futuro'

    }
  },
  mounted() {
    this.searchMovies();
  
  },
  methods: {
      searchMovies() {
      // Tramite Axios richiamo l'API dove otterrò l'array netflixMovie
      axios.get(this.getApi)
        .then(response => {
          this.netflixMovie = response.data.results;
          console.log(this.netflixMovie);
        })
        .catch(error => {
          console.log(error)
        })
    },
    query(text) {
      this.textToSearch = text;
      this.textToSearch = this.textToSearch.replace(" ", "+")
      this.searchMovies();
    }
  }
}

</script>

<style lang="scss">
@import './style/common.scss';
@import 'bootstrap';
</style>
