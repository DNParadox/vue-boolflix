<template>
  <div id="app">
    <myHeader @searchText="query" />
    <MyMain :netflixMovie="this.netflixMovie"  :netflixSeries="this.netflixSeries" />
  </div>
</template>

<script>
import myHeader from './components/myHeader.vue';
import MyMain from './components/myMain.vue';
import axios from 'axios'


export default {
  name: 'App',
  components: {
    // Componenti del mio sito per poter strutturare al meglio la pagina
    myHeader,
    MyMain
  },
  data() {
    return {
      textToSearch: "",
      // Array necessari al corretto funzionamento di myMain, li richiameremo tramite "props"
      netflixMovie: [],
      netflixSeries: [],
      // Semplificazione della chiamata Axios
      key: 'f86ac59dbbef3085387cb106cf5cea17'
    }
  },
  mounted() {
    this.searchMovies();
    this.searchSeries();
  },
  methods: {
    // Funzione per generare un Array di netflixMovie grazie ad Axios
    searchMovies() {
      if (this.textToSearch !== "") {
        // Tramite Axios richiamo l'API dove otterrò l'array netflixMovie
        axios.get(`https://api.themoviedb.org/3/search/movie?api_key=${this.key}&query=${this.textToSearch}&language=it-IT`)
          // Necessario al corretto funzionamento di Axios. Ci darà indietro il risultato dell'Arrray
          .then(response => {
            this.netflixMovie = response.data.results;
            console.log(this.netflixMovie);
          })
          // In caso di errori segnalerà in console
          .catch(error => {
            console.log(error)
          })
      }
    },
    // Funzione per generare un Array di netflixSeries grazie ad Axios
    searchSeries() {
      if (this.textToSearch !== "") {
        axios.get(`https://api.themoviedb.org/3/search/tv?api_key=${this.key}&query=${this.textToSearch}&language=it-IT`)
          .then(response => {
            this.netflixSeries = response.data.results;
            console.log(this.netflixSeries);
          })
          // In caso di errori segnalerà in console
          .catch(error => {
            console.log(error)
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
