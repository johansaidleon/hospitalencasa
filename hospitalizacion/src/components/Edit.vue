<template>
    <table align="left">
        <h1>EDICION</h1>
        <tr>
        <th scope="col"> ID</th>
        <th scope="col ">NOMBRE </th>
        <th scope="col">DIRECCION</th>
    </tr>
     <tr>
         <td>
            <input type="text" id="id" name= "id" v-model= "Lista.id">
        </td>
        <td>
            <input type="text" id="nombre" name="nombre" v-model= "Lista.nombre">
        </td>
        <td>
            <input type="text" id="nombre" name="nombre" v-model= "Lista.direccion">
        </td>
    </tr>
        <tr>
            <button v-on:click="editar() ">EDITAR</button>
        </tr>
    </table>
</template>
<script>
    import axios from 'axios';

    export default {
        name: "Edit",
        data() {
            return {
                Lista: [],
            }
        },
        methods: {
          editar () {
            let post = {
                "id": this.Lista.id,
                "nombre": this.Lista.nombre,
                "direccion": this.Lista.direccion,
            }
            axios.put("http://127.0.0.1:8000/api/entidad/" + this.$route.params.id + "/", post).then((result)=>{
            console.log(result);
                this.Lista.id="";
                this.Lista.nombre="";
                this.Lista.direccion="";
            })
        },
    },
    mounted () {
        let id = this.$route.params.id;
        let direccion = "http://127.0.0.1:8000/api/entidad/"
        axios.get (direccion + id).then (data => {
            this.Lista = data.data;
        })
    },
}
</script>
