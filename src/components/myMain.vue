<template>

    <main>
        <div class="container-fluid">
            <div class="column d-flex">

                <div class="card" v-for="(element, index) in netflixMovie" :key="element.id" :movie="element">

                    <img class="film_poster" :src="getImg(netflixMovie[index].poster_path)"
                        :alt="netflixMovie[index].title">
                    <div class="title">Titolo: {{ netflixMovie[index].original_title }} </div>
                    <img class="flags" :src="getFlags(netflixMovie[index].original_language)"
                        :alt="'language: ' + netflixMovie[index].original_language">
                     <div class="rating">Voto: <i class="fa-solid fa-star star-space"
                            :class="{'star': n <= getNemesis(netflixMovie[index].vote_average)}" v-for=" n in 5"
                            :key="n"></i> </div>

                </div>



                <div class="card" v-for="(element, index) in netflixSeries" :key="element.id" :series="element">

                    <img class="film_poster" :src="getImg(netflixSeries[index].poster_path)"
                        :alt="netflixSeries[index].title">
                    <div class="title">Titolo: {{ netflixSeries[index].title }} </div>
                    <img class="flags" :src="getFlags(netflixSeries[index].original_language)"
                        :alt="'language: ' + netflixSeries[index].original_language">
                    <div class="rating">Voto: <i class="fa-solid fa-star"
                            :class="{'star': z <= getNemesis(netflixSeries[index].vote_average)}" v-for=" z in 5"
                            :key="z"></i> </div>

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
        netflixSeries: Array,
    },
    data() {
        return {


        }
    },
    methods: {

        //  Prendiamo da un api di Bandiere le bandiere necessarie
        getFlags(country) {
            if (country == 'en') {
                country = "gb";
            } else if (country == 'ja') {
                country = "jp";
            } else if (country == 'hi') {
                country = "in";
            } else if (country == 'cs') {
                country = "cz";
            } else if (country == 'ko') {
                country = "kr";
            } else if (country == 'sv') {
                country = "ch";
            } else if (country == 'fa') {
                country = "af";
            }
            // poi ritorno la bandiera 
            return `https://countryflagsapi.com/png/${country}`;
        },
        getImg(path) {
            if (path === null) {
                return 'https://image.tmdb.org/t/p/w342/wwemzKWzjKYJFfCeiB57q3r4Bcm.png'
            }
                return `https://image.tmdb.org/t/p/w342${path}`
        },
        getNemesis(star) {
            // divido star che è un valore di 1 a 10 / 2
            const stars = star/ 2;
            // Arrotondo il numero
            return Math.round(stars);
        }
        
    }
}
</script>

<style>
.card {
    margin-right: 2rem;
}

.star {
    color: goldenrod;
}
</style>