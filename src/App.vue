<template>
  <div>
    <h1>Hello world</h1>
  </div>
</template>

<script>
  export default {
    name: 'App',
    data(){
      return {
        
      }
    }
  }
</script>

<style lang="scss" scoped>
@use './assets/styles/partials/variables' as *;

h1 {
    color: $font-color;
}

</style>
