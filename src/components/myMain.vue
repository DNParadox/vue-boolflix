<template>
    <main>
        <div class="container-fluid">
            <div class="column d-flex">
                <!-- Richiamiamo tramite v-for per l'array NetflixMovie -->
                <div class="card" v-for="(element, index) in netflixMovie" :key="element.id" :movie="element">
                    <!-- Da qui abbiammo accesso alle varie chiavi per poter stampare a schermo -->
                    <img class="film_poster" :src="getImg(netflixMovie[index].poster_path)"
                        :alt="netflixMovie[index].title">

                    <!-- All'hover, la carta verrà opacizzatà e visualizzerà il suo contenuto -->
                    <div class="covered">

                        <div class="title">Titolo: {{ netflixMovie[index].title }} </div>
                        <div class="title" >Titolo originale: {{ netflixMovie[index].original_title }} </div>
                        <div class="language">
                            <span> Lingua: </span>
                            <img class="flags" :src="getFlags(netflixMovie[index].original_language)"
                                :alt="'language: ' + netflixMovie[index].original_language">
                        </div>
                        <div class="rating">Voto: <i class="fa-solid fa-star starbefore"
                                :class="{ 'star': n <= getNemesis(netflixMovie[index].vote_average) }" v-for=" n in 5"
                                :key="n"></i> </div>
                        <div class="overview">Overview: {{ netflixMovie[index].overview }} </div>
                    </div>
                </div>


                <!-- Richiamiamo tramite v-for per l'array NetflixSeries -->
                <div class="card" v-for="(element, index) in netflixSeries" :key="element.id" :series="element">
                    <!-- Da qui abbiammo accesso alle varie chiavi per poter stampare a schermo -->
                    <img class="film_poster" :src="getImg(netflixSeries[index].poster_path)"
                        :alt="netflixSeries[index].title">
                    <div class="covered">
                    <div class="title">Titolo: {{ netflixSeries[index].title }} </div>
                    <div class="title">Titolo originale: {{ netflixSeries[index].original_title }} </div>
                    <div class="language">
                        <span> Lingua: </span>
                        <img class="flags" :src="getFlags(netflixSeries[index].original_language)"
                        :alt="'language: ' + netflixSeries[index].original_language">
                    </div>
                   
                    <div class="rating">Voto: <i class="fa-solid fa-star"
                            :class="{ 'star': z <= getNemesis(netflixSeries[index].vote_average) }" v-for=" z in 5"
                            :key="z"></i> </div>
                    <div class="overview">Overview: {{ netflixSeries[index].overview }} </div>

                    </div>
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
        // Con questi due comandi richiamo i due Array stipati in App.vue
        netflixMovie: Array,
        netflixSeries: Array,
    },
    methods: {
        //  Prendiamo da un api di Bandiere le bandiere necessarie alla visualizzazione a schermo
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
        // Funzione necessaria alla modifica di poster_path
        getImg(path) {
            if (path === null) {
                // Se il titolo non avrà poster_path, quindi sarà null darà un immagine scelta da noi
                return 'https://image.tmdb.org/t/p/w342/wwemzKWzjKYJFfCeiB57q3r4Bcm.png'
            }
            // Diversamente, se path contiene una stringa stamperà l'immagine in essa
            return `https://image.tmdb.org/t/p/w342${path}`
        },
        // Citazione a RE3 necessaria. Questa funzione fa in modo che io ottenga le stelle anziché un punteggio numerico
        getNemesis(star) {
            // divido star che è un valore da 1 a 10 e lo divido per 2
            const stars = star / 2;
            // Arrotondo il numero
            return Math.round(stars);
        },
    }
}
</script>

<style>
.column {
    flex-wrap: wrap;
    overflow-x: scroll;
}

.card {
    margin-right: 2rem;
    border: none !important;
    margin-bottom: 1rem;
}

.covered {
    display: none;
}

.card:hover .covered {
    display: block;
    position: absolute;
    width: 100%;
    height: 100%;
    color: white;
    background: rgba(0, 0, 0, 0.9);
}

.starbefore {
    color:grey
}
.star {
    color: goldenrod;
}

.flags {
    width: 40px;
}
</style>