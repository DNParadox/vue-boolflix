<template>

    <main>
        <div class="container-fluid">
            <div class="column d-flex">
                <div class="card" v-for="(element, index) in netflixMovie" :key="index" :movie="element">

                    <div class="title"> {{ netflixMovie[index].original_title }} </div>
                    <div class="lang"> {{ netflixMovie[index].original_language }}</div>
                    <div class="rating"> {{ netflixMovie[index].vote_average }} </div>

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
            getApi: 'https://api.themoviedb.org/3/search/movie?api_key=e99307154c6dfb0b4750f6603256716d&query=ritorno+al+futuro'
        }
    },
}
</script>

<style>
.card {
    width: calc(100% / 3);
    margin-right: 2rem;
}
</style>