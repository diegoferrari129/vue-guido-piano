<script>
  import Header from './components/layouts/Header.vue';
  import Footer from './components/layouts/Footer.vue';
  import { store } from './store';

  export default {

    components:{
      Header,
      Footer
    },

    data() {
      return {
        store,
      }
    },

  }
</script>

<template>
  <Header :menu="store.menuItems"/>
  <router-view></router-view>
  <Footer />
</template>

<style lang="scss">
  @import './styles/generals.scss';
</style>
