<script setup>
    const props = defineProps({
        articulo:{
            type: Object,
            required: true,
        }
    })

    defineEmits(['agregar-carrito'])
</script>

<template>
    <div class="col-md-6 col-lg-4 row align-items-center">
        <div class="col-4">
          <img width="200px"
          class="img-fluid" 
          v-bind:src="'/img/'+articulo.imagen+'.jpg' ">
        </div>
        <div class="col-8">
          <h3 class="nombre fs-4 fw-bold text-uppercase">{{articulo.nombre}}</h3>
          <p>{{ articulo.descripcion }}</p>
          <p><b>Proveedor: </b>{{ articulo.marca }}</p>
          <p class="fw-black precio fs-3">Lps {{articulo.precio}}</p>
          <button type="button" 
            class="btn btn-danger w-100" 
            @click="$emit('agregar-carrito', articulo)">
            Agregar al Carrito
          </button>
        </div>
    </div>
</template>

<style>
    img{
        width: 200px;
    }
</style>