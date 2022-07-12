<template>
  <div id="app">
      <myHeader/>
      <MyMain/>
  </div>
</template>

<script>
import myHeader from './components/myHeader.vue';
import MyMain from './components/myMain.vue';


export default {
  name: 'App',
  components: {
    myHeader,
    MyMain
}
}
</script>

<style lang="scss">
@import './style/common.scss';
@import 'bootstrap';
</style>
