<template>
  <div>
    <div id="nav">
      <img id="firo" src="@/assets/firo.jpg" alt="firo" width="60px" height="60px">
    </div>
  </div>
</template>

<script>
export default {
    name: 'Navbar'
};
</script>
<style scoped>
  #nav{
    position: fixed;
    top:0;
    left:0;
    height: 70px;
    width: 100%;
    z-index: 1;
    /* background: rgb(254, 128, 149) */
    background: #DB2955;
  }
  #firo{
    float: left;
    margin-top: 5px;
    margin-left: 5px;
  }
</style>
