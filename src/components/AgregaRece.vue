<template>
<div id="Receta">
  <div id="sidebar">
    <h3>{{titulo}}</h3>
    <div class="input-group mb-3">
      <div class="input-group-prepend">
        <span class="input-group-text" id="basic-addon1">❀</span>
      </div>
      <input v-model="nuevoTitulo" type="text" class="form-control" placeholder="Nombre del Postre..." aria-label="Dessert" aria-describedby="basic-addon1">
    </div>

    <div class="input-group mb-3">
      <div class="input-group-prepend">
        <span class="input-group-text" id="basic-addon1">❀</span>
      </div>
      <input v-model="nuevoUsuario" type="text" class="form-control" placeholder="Ingrese su nombre..." aria-label="Username" aria-describedby="basic-addon1">
    </div>

    <div class="input-group">
      <textarea v-model="nuevaReceta" class="form-control" aria-label="With textarea" placeholder="Escriba los ingredientes aqui..."></textarea>
    </div>

    <br>==============
    <hr>
    <input id="inp" type="text">
    <button id="agregar" @click="agregarTodo">agregar</button>
    <button id="editar" @click="editarTarjeta">editar</button>
    <button id="cancelar" @click="cancelar">cancelar</button>
  </div>

  <div id="recipes">
    <form class="form-inline">
      <input id="buscar" v-model="search" class="form-control mr-sm-2" type="search" placeholder="Buscar" size="100%">
    </form>
    <div class="container">
      <div class="row">
        <div id="card" class="card mb-4" style="width: 18rem" v-for="(titulo,index) in busqueda" :key="titulo.id">
          <img src="@/assets/Miira.jpg" class="card-img-top">
          <div class="card-body">
            <h5 id="NomTit" class="card-title">{{titulo.lsnuevoTitulo}}</h5>
            <h6 id="NomUss">{{titulo.lsnuevoUsuario}}</h6>
            <p id="ReceUss" class="card-text">{{titulo.lsnuevaReceta}}</p>
            <button id="editarCopy" class="btn-info" @click="editarCopy(index)">✓</button>
            <button id="eliminar" class="btn-danger" @click="eliminar(index)">⌫</button>
          </div>
        </div>
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
      nuevaReceta: "",
      search: ""
    };
  },
  methods: {
    limpiar() {
      this.nuevoUsuario = "";
      this.nuevoTitulo = "";
      this.nuevaReceta = "";
    },
    setLocStor() {
      localStorage.setItem("postres-vue", JSON.stringify(this.recetas));
    },
    vistaBotonesDesaparecer() {
      document.getElementById("agregar").style.display = "block";
      document.getElementById("editar").style.visibility = "hidden";
      document.getElementById("cancelar").style.visibility = "hidden";
    },
    vistaBotonesAparecer() {
      document.getElementById("agregar").style.display = "none";
      document.getElementById("editar").style.visibility = "visible";
      document.getElementById("cancelar").style.visibility = "visible";
    },
    jsonaUss(index) {
      this.nuevoTitulo = this.recetas[index].lsnuevoTitulo;
      this.nuevoUsuario = this.recetas[index].lsnuevoUsuario;
      this.nuevaReceta = this.recetas[index].lsnuevaReceta;
    },
    ussaJson(index) {
      this.recetas[index].lsnuevoTitulo = this.nuevoTitulo.trim();
      this.recetas[index].lsnuevoUsuario = this.nuevoUsuario;
      this.recetas[index].lsnuevaReceta = this.nuevaReceta;
    },
    agregarTodo() {
      if (this.nuevoTitulo == '' || this.nuevoUsuario == '' || this.nuevaReceta == '') {
        alert('MIERDA!!!!')
        return;
      }

      if (this.nuevoTitulo.trim().length < 4) {
        alert('MIERDA!!!!, tienes menos de 4 caractes no seas flojo')
        return;
      }

      // if (this.nuevoTitulo != '' && this.nuevoUsuario != '' && this.nuevaReceta != '') {
      this.recetas.push({
        lsnuevoTitulo: this.nuevoTitulo.trim(),
        lsnuevoUsuario: this.nuevoUsuario,
        lsestado: false,
        lsnuevaReceta: this.nuevaReceta
      });
      this.limpiar();
      this.setLocStor();
      // } else {
      //   alert('MIERDA!!!!')
      // }
    },
    editarCopy(index) {
      this.jsonaUss(index);
      document.getElementById("inp").value = index;
      this.vistaBotonesAparecer();
    },
    editarTarjeta() {
      let index = document.getElementById("inp").value;
      //let datosNuevos = JSON.parse(localStorage.getItem("postres-vue"));
      this.ussaJson(index);
      this.vistaBotonesDesaparecer();
      this.limpiar();
      this.setLocStor();
    },
    eliminar(index) {
      this.recetas.splice(index, 1);
      this.setLocStor();
    },
    cancelar() {
      this.limpiar();
      this.setLocStor();
      this.vistaBotonesDesaparecer();
    }
  },
  computed: {
    busqueda() {
      return this.recetas.filter(titulo =>
        titulo.lsnuevoTitulo.toLowerCase().includes(this.search.toLowerCase())
      );
    }
  },
  //Proceso LocalStorage
  created: function() {
    // let datosDB = JSON.parse(localStorage.getItem("postres-vue"));
    // if (datosDB === null) {
    //   this.recetas = [];
    // } else {
    //   this.recetas = datosDB;
    // }
    let datosDB = JSON.parse(localStorage.getItem("postres-vue"));
    this.recetas = datosDB === null ? [] : datosDB;
  }
}
</script>

<style scoped>
#Receta {
  background: pink;
  margin-top: 70px;
}

#sidebar {
  position: fixed;
  top: 0;
  left: 0;
  background: rgb(255, 211, 215);
  width: 30%;
  height: calc(100vh - 70px);
  margin-top: 70px;
  padding-left: 8px;
  padding-right: 8px;
}

#buscar {
  width: 100%;
  margin-left: 10px;
}

#recipes {
  background: rgb(211, 211, 211);
  width: 70%;
  margin-left: 30%;
  display: inline-block;
  min-height: calc(100vh - 70px);
}

#recipes .row {
  justify-content: center;
}

.card {
  margin: 10px;
  margin-top: 20px;
  display: block;
  background: #fdf5bf;
}

#editar {
  background: rgb(210, 68, 141);
  color: white;
  margin-right: 6px;
  border-radius: 8px;
  visibility: hidden;
}

#cancelar {
  background: rgb(210, 68, 141);
  color: white;
  border-radius: 8px;
  visibility: hidden;
}

#editarCopy {
  background: rgb(255, 211, 215);
  color: gray;
  border-color: rgb(255, 211, 215);
  margin-right: 5px;
  border-radius: 15px;
}

#eliminar {
  background: #db2955;
  border-radius: 15px;
}

#agregar {
  color: white;
  background: rgb(210, 68, 141);
  border-radius: 8px;
  visibility: visible;
}

#inp {
  display: none;
}

#nomTit {
  visibility: visible;
}

#nomPost {
  visibility: visible;
}
</style>
