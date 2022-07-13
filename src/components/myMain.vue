<template>

    <main>
        <div class="container-fluid">
            <div class="column d-flex">

                <div class="card" v-for="(element, index) in netflixMovie" :key="element.id" :movie="element">

                    <div class="title">Titolo:  {{ netflixMovie[index].original_title }} </div>
                    <div class="lang"> Lingua: {{ netflixMovie[index].original_language }}</div>
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
}
</script>

<style>
.card {
    margin-right: 2rem;
}
</style>