@extends('layouts.app')
<template>
<div class="container">
    <div class="row">
        <div class="col">
            <h1>Inventario</h1>
        </div>
    </div>
    <div class="row">
        <div class="col-1">
            <button class="btn btn-primary" v-on:click="btnPistolear">Pistolear</button>
            
        </div>
        <div class="col">
            <button class="btn btn-primary" v-on:click="btnProducto">Agregar Stock</button>
        </div>
        
    </div>
    <div class="row">
        <div class="col-md-12 my-5">
            <div class="card">
                <table class="table">
                <thead>
                    <tr>
                        <th>Stock</th>
                        <th>Despachado</th>
                        <th>Nombre Producto</th>
                    </tr>
                </thead>
                <tbody>
                    <tr v-for="evento in eventos" :key="evento">
                        <td>{{ evento.stock }}</td>
                        <td>{{ evento.despachado }}</td>
                        <td>{{ evento.nombre_producto }}</td>
                    </tr>
                </tbody>
            </table>
            </div>
            
        </div>
        
    </div>
    
</div>
</template>

<script>
import axios from "axios";
export default {
    name: 'table-evento-list-row',
    mounted: function () {
      this.getproducto2();
      console.log('mounted: got here')
    },
    data(){
        return{
            message:'',
            message2:'',
            producto:'',
            estado:'',
            eventos:[]
        }
    },
  created() {
    
  },
  methods:{
      
    async guardar() {
      axios.post("http://127.0.0.1:8000/pistolear/"+this.message).then((result) => {
        this.message = '';
        this.message2 = 'despachado';
        console.log(result.data);
    })
    },

    async getproducto(){
        axios.get("http://127.0.0.1:8000/getpistolear/"+this.message).then((result) => {
        this.producto = result.data.nombre+result.data.descripcion;
        this.message2 = '';
        this.estado = result.data.estado;
        this.message3 = new Date(Date.parse(result.data.fecha)).toLocaleDateString('es-CL');
        console.log(result.data);
    })
    },
    async getproducto2(){
        axios.get("http://127.0.0.1:8000/productosall").then((result) => {
        this.eventos = result.data;
        console.log(result.data);
    })
    },
    btnPistolear(){
        window.location.href = "pistolear";
    },
    btnProducto(){
        window.location.href = "agregarproducto";
    }
  }
};
</script>

<style scoped lang="scss">
</style>