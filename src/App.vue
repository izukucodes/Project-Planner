<template>
  <h1 class="title">Project Planner</h1>
  <Navbar />
  <router-view />
</template>
<script>
import Navbar from "./components/Navbar.vue";
export default {
  components: { Navbar },
};
</script>
<style>
body {
  background: #f2f2f2;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  max-width: 600px;
  margin: 0 auto;
  color: #555;
}
.title {
  text-align: center;
  margin: 50px auto;
  font-family: sans-serif;
  text-transform: uppercase;
  font-size: 30px;
  color: #777;
}
</style>
