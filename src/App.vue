<script>
import Header from './components/layouts/Header.vue';
import { store } from './store';

export default {

  components:{
    Header,
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
</template>

<style lang="scss">
  @import './styles/generals.scss';
</style>
