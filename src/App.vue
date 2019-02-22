<template>
  <div id="app">
      <Navbar></Navbar>
      <AgregaRece></AgregaRece>
      <Footer></Footer>
    </div>
</template>

<script>
import Navbar from "./components/Navbar.vue";
import AgregaRece from "./components/AgregaRece.vue";
import Sidebar from "./components/Sidebar.vue";
import Recipes from "./components/Recipes.vue";
import Footer from "./components/Footer.vue";


export default {
  name: "app",
  components: {
    Navbar,
    Sidebar,
    Recipes,
    AgregaRece,
    Footer
  }
};
</script>

