<template>
  <div id="app">
    <Home v-if="currentPage === 'Home'" msg="Fast Word Finder" />
    <About v-if="currentPage === 'About'" />
  </div>
</template>

<script>
import Home from "./pages/Home.vue";
import About from "./pages/About.vue";

export default {
  name: "App",
  components: {
    Home,
    About,
  },
  data() {
    return {
      currentPage: "About",
    };
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin: 0px;
}

body {
  margin: 0px;
}
</style>
