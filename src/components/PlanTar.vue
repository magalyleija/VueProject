<script>
export default {
  name: "PlanTar"

};
</script>
<style scoped>
  .btn-info{
    margin-right: 4px;
  }
  #PlanTar{
    background: rgb(148, 247, 254);
  }
</style>

<template>
  <div id="PlanTar">
    <div class="card" style="width: 18rem;" v-for="item of recetas">
      <img src="@/assets/Miira.jpg" class="card-img-top" alt="">
      <div class="card-body">
        <h5 id="NomPost" class="card-title">Card title</h5>
        <h6 id="NomUss">Usuario</h6>
        <p id="ReceUss" class="card-text">
          Some quick example text to build on the card title and make up the bulk of the card's content.</p>
        <!--<a href="#" class="btn btn-primary">Go somewhere</a>-->
        <button class="btn-info">✓</button>
        <button class="btn-danger">⌫</button>
      </div>
    </div>
  </div>
</template>



