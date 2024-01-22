<template>
  <AppHeader />
  <router-view></router-view>
</template>

<script>
import axios from "axios";
import { store } from "./store";
import AppHeader from "./components/AppHeader.vue";
  export default {
    name: 'App',
    components: {
      AppHeader,
    },
    data(){
      return {
        store,
      }
    },
    methods: {
      getApiTest(){
        axios.get(this.store.apiUrl + "projects").then((res) => {
          console.log(res.data);
        }).catch
      }
    },
    mounted() {
      
    }
  }
</script>

<style lang="scss" scoped>
@use './assets/styles/partials/variables' as *;



</style>
