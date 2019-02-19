<template>
  <div class="mt-3" id="Receta">
    <h2>{{titulo}}</h2>
    <div class="input-group mb-3">
      <div class="input-group-prepend">
        <span class="input-group-text" id="basic-addon1">❀</span>
      </div>
      <input v-model="nuevoTitulo"
        v-on:keyup.enter="agregarTitulo"
        type="text"
        class="form-control"
        placeholder="Nombre del Postre..."
        aria-label="Dessert"
        aria-describedby="basic-addon1">
    </div>
    <div class="input-group mb-3">
      <div class="input-group-prepend">
        <span class="input-group-text" id="basic-addon1">❀</span>
      </div>
      <input v-model="nuevoUsuario"
        v-on:keyup.enter="agregarUsuario"
        type="text"
        class="form-control"
        placeholder="Ingrese su nombre..."
        aria-label="Username"
        aria-describedby="basic-addon1">
    </div>
    <div class="input-group">
      <textarea v-model="nuevaReceta"
        class="form-control"
        aria-label="With textarea"
        placeholder="Escriba los ingredientes aqui...">
      </textarea>
    </div>
    <br>
    <input type="file">
    <hr>
    
    <button id="agregar" @click="agregarTodo">Agregar</button>
<!--<h6>{{nuevoUsuario}}</h6>-->
<!--<h6>{{nuevoTitulo}}</h6>-->
<!--<h6>{{nuevaReceta}}</h6>-->
    <form class="form-inline">
        <input id="buscar" class="form-control mr-sm-2" type="search" placeholder="Buscar">
        <button class="btn btn-outline-success my-2 my-sm-0" type="submit"
        @click="buscarDatos">Search</button>
      </form>
    <div>
      <div id="card" class="card" style="width: 18rem" v-for="(item,index) of recetas" :key="item.id">
        <img src="@/assets/Miira.jpg" class="card-img-top">
        <div class="card-body">
          <h5 id="NomPost" class="card-title">{{item.lsnuevoTitulo}}</h5>
          <h6 id="NomUss">{{item.lsnuevoUsuario}}</h6>
          <p id="ReceUss"
            class="card-text"
          >{{item.lsnuevaReceta}}</p>
          <!--<a href="#" class="btn btn-primary">Go somewhere</a>-->
          <button class="btn-info" @click="editarTarjeta(index)">✓</button>
          <button class="btn-danger" @click="eliminar(index)">⌫</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "AgregaRece",
  data() {
    return {
      titulo: "Agrega tu receta",
      recetas: [],
      nuevoUsuario: "",
      nuevoTitulo: "",
      nuevaReceta: ""
    };
  },
  methods: {
    agregarTodo(){
      this.recetas.push({
        lsnuevoTitulo: this.nuevoTitulo,
        lsnuevoUsuario: this.nuevoUsuario,
        lsestado: false,
        lsnuevaReceta: this.nuevaReceta
      });
      //console.log(this.recetas);
      this.nuevoUsuario = "";
      this.nuevoTitulo = "";
      this.nuevaReceta = "";
      localStorage.setItem('postres-vue', JSON.stringify(this.recetas));
      
    },
    buscarDatos(){
      
    },
    editarTarjeta(index) {
      
    },
    eliminar(index) {
      this.recetas.splice(index, 1);
      localStorage.setItem('postres-vue', JSON.stringify(this.recetas));
    },
    
  },
  //Proceso LocalStorage
  created: function() {
    let datosDB = JSON.parse(localStorage.getItem("postres-vue"));
    if (datosDB === null) {
      this.recetas = [];
    } else {
      this.recetas = datosDB;
    }
  }
};

/*agregarTitulo() {
      this.recetas.push({
        receTitulo: this.nuevoTitulo
      });
      this.nuevoTitulo = "";
      localStorage.setItem('postres-vue', JSON.stringify(this.recetas));
    },
    agregarUsuario() {
      //console.log('diste click ', this.nuevaReceta);
      this.recetas.push({
        nombre: this.nuevoUsuario,
        estado: false
      });
      //console.log(this.recetas);
      this.nuevoUsuario = "";
      localStorage.setItem('postres-vue', JSON.stringify(this.recetas));
    },
    agregarReceta() {
      this.recetas.push({
        nuevaReceta: this.nuevaReceta
      });
      this.nuevaReceta = "";
      localStorage.setItem('postres-vue', JSON.stringify(this.recetas));
    },
    
*/
</script>

<style>
#Receta {
  background: pink;
}
#buscar{
  margin-top: 15px
}
.card{
  margin: 10px;
  display: block;
}
</style>



