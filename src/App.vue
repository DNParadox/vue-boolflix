<template>
  <div id="app">
    <myHeader @searchText="query" />
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
      netflixSeries: [],
      key: 'f86ac59dbbef3085387cb106cf5cea17'
    }
  },
  mounted() {
    this.searchMovies();

  },
  methods: {
    searchMovies() {
      // Tramite Axios richiamo l'API dove otterrò l'array netflixMovie
      if (this.textToSearch !== "") {
        axios.get(`https://api.themoviedb.org/3/search/movie?api_key=${this.key}&query=${this.textToSearch}&language=it-IT`)
          .then(response => {
            this.netflixMovie = response.data.results;
            console.log(this.netflixMovie);
          })
          .catch(error => {
            console.log(error)
          })
      }
    },
    searchAllTvSeries() {
      // PER LE SERIE TV controllo se è la stringa è vuota cosi printo una pagina inziale
      if (this.textToSearch !== "") {
        axios.get(`https://api.themoviedb.org/3/search/movie?api_key=${this.key}&query=${this.textToSearch}&language=it-IT`)
          .then(response => {
            this.serieArray = response.data.results;
          })
      }
    },
    query(text) {
      this.textToSearch = text;
      this.textToSearch = this.textToSearch.replace(" ", "+")
      this.searchMovies();
      this.searchSeries();
    }
  },
}
</script>

<style lang="scss">
@import './style/common.scss';
@import 'bootstrap';
</style>
