<template>
  <NavBar />
  <router-view />
</template>

<script>
import NavBar from './components/NavBar.vue';

export default {
  components: { NavBar }
}
</script>

<style>
body{
  background-color: #f2f2f2;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #555;
  max-width: 600px;
  margin: 0 auto;

}
.all-border {
   border: 2px solid #e90074 !important;
}
</style>
