<template>
  <NavVue></NavVue>
  <router-view/>
</template>

<script>
  import NavVue from "./components/Nav.vue";
  export default{
   components:{
    NavVue
   }
  }
</script>
<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  max-width: 600px;
  margin: 0 auto;
  color: #2c3e50;
}


</style>
