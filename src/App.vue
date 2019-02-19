<template>
  <div id="app">
    <div id="nav">
      <Navbar></Navbar>
      <AgregaRece></AgregaRece>
      
    </div>
  </div>
</template>

<script>
import Navbar from "./components/Navbar.vue";
import AgregaRece from "./components/AgregaRece.vue";
//import PlanTar from "./components/PlanTar.vue";

export default {
  name: "app",
  components: {
    Navbar,
    AgregaRece
  }
};
</script>

