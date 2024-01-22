<template>
  <div>
    <h1>Hello world</h1>
  </div>
  <router-view></router-view>
</template>

<script>
import axios from "axios";
import { store } from "./store";
  export default {
    name: 'App',
    data(){
      return {
        store,
      }
    },
    methods: {
      getApiTest(){
        axios.get(this.store.apiUrl + "projects").then((res) => {
          console.log(res.data);
        })
      }
    },
    mounted() {
      this.getApiTest();
    }
  }
</script>

<style lang="scss" scoped>
@use './assets/styles/partials/variables' as *;

h1 {
    color: $font-color;
}

</style>
