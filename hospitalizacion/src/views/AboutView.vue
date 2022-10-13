<template>
  <table align="left">

    <div id="Entidad"> <h1>ENTIDAD</h1> </div>
    <tr>
      <th scope="col"> ID</th>
      <th scope="col">NOMBRE</th>
      <th scope="col">DIRECCTON</th>|
    </tr>
    <tr>
      <td>
        <input type="text" id="id" name="id" v-model="post.id">
      </td>
      <td>
        <input type="text" id="nombre " name="nombre" v-model="post.nombre">
      </td>
      <td>
        <input type="text " id="direccion" name="direccion " v-model="post.direccion">
      </td>
    </tr>
    <tr>

      I <button v-on:click="registrar () ">CREAR</button>
    </tr>
    <br><br><br>
    <tr>
      <th scope="col">ID</th>
      <th scope="col">NOMBRE</th>
      <th scope="col">DIRECCION</th>
    </tr>
    <tr v-for="i in Lista">
      <td>{{i.id}}</td>
      <td>{{i.nombre}}</td>
      <td>{{i.direccion}}</td>
      <td>
        <button v-on:click="editar (i.id) ">DELETE</button>
      </td>
      <td>
        <button v-on:click="editar (i.id) ">UPDATE</button>
      </td>
    </tr>
  </table>
</template>

<script>
import axios from 'axios';

export default {
  name: "AboutView",
  data() {
    return {
      post: {
        id: 0,
        nombre: "",
        direccion: "",
      },
      lista: "",

    }
  },
  methods: {
    registrar() {

      axios.post("http://127.0.0.1:8000/api/entidad/", this.post).then (
        result=>{
          alert(result)
        }
      )
    },
    editar(id) {
      console.log(id)
      this.$router.push("edit/" + id);
    },
    eliminar(id) {
      console.log(id)
      axios.delete("http://127.0.0.1:8000/api/entidad/" + id ).then(result => {
        this.created()
        console.log(result);
      })
    },

  },
  created(){
    let direccion = "http://127.0.0.1:8000/api/entidad/";
      axios.get(direccion).then(data => {
        this.Lista = data.data;
      })
  },

  updated() {
      let direccion = "http://127.0.0.1:8000/api/entidad/";
      axios.get(direccion).then(data => {
        this.Lista = data.data;
      })
    },

  mounted() {
    let direccion = "http://127.0.0.1:8000/api/entidad/";
    axios.get(direccion).then(data => {
      this.Lista = data.data;
      console.log(data);
    })
  },
} 
</script>

<style>

</style>

