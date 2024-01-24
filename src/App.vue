<template>
  <div class="main-container vh-100 w-100 overflow-hidden">
    <AppHeader />
    <div class="vh-100 my-container">
      <router-view :key="$route.path"></router-view>
    </div>
    <AppFooter />
  </div>
    
</template>

<script>
import axios from "axios";
import { store } from "./store";
import AppHeader from "./components/AppHeader.vue";
import AppFooter from "./components/AppFooter.vue";
  export default {
    name: 'App',
    components: {
      AppHeader,
      AppFooter,
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

.my-container {
  padding-top: 60px;
}

.main-container {
  background: radial-gradient(ellipse at bottom, #0d1d31 0%, #0c0d13 100%);
}

</style>
