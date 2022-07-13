<template>

    <main>
        <div class="container-fluid">
            <div class="column d-flex">

                <div class="card" v-for="(element, index) in netflixMovie" :key="element.id" :movie="element">

                    <div class="title">Titolo:  {{ netflixMovie[index].original_title }} </div>
                    <img class="flags" :src="getFlags(netflixMovie[index].original_language)" :alt="'language: ' + netflixMovie[index].original_language">
                    <div class="rating">Voto:  {{ netflixMovie[index].vote_average }} </div>

                </div>

            </div>
        </div>
    </main>
</template>

<script>
export default {
    name: 'myMain',
    components: {

    },
    props: {
        netflixMovie: Array,
    },
    data() {
        return {
            netflixArr: [],
        }
    },
    methods: {

     //  Prendiamo da un api di Bandiere le bandiere necessarie
    getFlags(country){
      
      if(country == 'en'){
        country = "gb";
      } else if(country == 'ja'){
        country = "jp";
      } else if(country== 'hi'){
        country = "in";
      } else if(country == 'cs'){
        country = "cz";
      } else if(country == 'ko'){
        country = "kr";
      } else if(country == 'sv'){
        country = "ch";
      } else if(country == 'fa'){
        country = "af";
      }
      // poi ritorno la bandiera 
      return `https://countryflagsapi.com/png/${country}`;
    },
    }
}
</script>

<style>
.card {
    margin-right: 2rem;
}
</style>