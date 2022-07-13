<template>
    <header>
        <div class="container-fluid ">

            <nav class="d-flex justify-content-between align-items-center">
                <div class="mylogo">
                    <h1> BOOLFLIX</h1>
                </div>
                <div class="searchbar">

                    <label for="searchbar"></label>
                    <input type="text" id="searchbar" placeholder="Cerca il tuo film"
                        v-model="query"
                        @keypress.enter="searchbar">
                    <button class="btn btn-success" @click.prevent="searchbar">Submit</button>

                </div>
            </nav>

        </div>
    </header>
</template>


<script>
export default {
    name: 'myHeader',
    data() {
        return {
            query: "",
        }
    },
    methods: {
        searchbar() {
            this.$emit('searchText', this.query);
            console.log(this.query);
            this.query = "";
        }
    }
}
</script>


<style scoped lang="scss">
nav {
    height: 100%;
}
</style>