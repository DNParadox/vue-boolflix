<template>
    <header>
        <div class="container-fluid ">
         
        <nav class="d-flex justify-content-between align-items-center">
                <div class="mylogo">
               <h1> BOOLFLIX</h1>
            </div>
            <div class="searchbar">
                
                <label for="searchbar"></label>
                <input type="text" id="searchbar" placeholder="Cerca il tuo film" v-model="query" >

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
            $emit('search', this.query);
            this.query = "";    
        }
    } 

}
</script>


<style scoped lang="scss">
    nav{
        height: 100%;
    }

</style>