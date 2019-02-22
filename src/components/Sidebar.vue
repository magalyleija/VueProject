<template>
  <div>
    <p>Hola de sidebar</p>
  </div>
</template>

<script>
export default {
    name: 'Sidebar',
    props: ['titulo']
};
</script>
<style scoped>
  div{
      position: fixed;
      top:0;
      left: 0;
      background: yellow;
      width: 30%;
      height: calc(100vh - 70px);
      margin-top: 70px;
  }
</style>
