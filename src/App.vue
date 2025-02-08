<script setup>
  import { ref, reactive, onMounted} from 'vue'
  import { db } from './data/Articulos.js'
  import Articulo from './components/Articulo.vue'
  import Header from './components/Header.vue'
  import Footer from './components/Footer.vue'

  const articulos = ref([])
  const carrito = ref([])
  const articulo = ref({})

  onMounted( () =>{
    articulos.value = db;
    articulo.value = db[3];
  })

  const agregarCarrito = (articulo) =>{

    const existeCarrito = carrito.value.findIndex(producto => producto.id === articulo.id)
    
    if(existeCarrito >= 0){
      carrito.value[existeCarrito].cantidad++
    }else{
      articulo.cantidad = 1
      carrito.value.push(articulo);
    }
  }

  const decrementarCantidad = (id) => {
    const index = carrito.value.findIndex(producto => producto.id === id)
    if(carrito.value[index].cantidad <= 1) return 
    carrito.value[index].cantidad--
  }

  const incrementarCantidad = (id) => {
    const index = carrito.value.findIndex(producto => producto.id === id)
    carrito.value[index].cantidad++
  }

  const eliminarProducto = (id) => {
    carrito.value = carrito.value.filter(producto => producto.id !== id)
  }

  const vaciarCarrito = () => {
    carrito.value = []
  }
</script>

<template>

<body>
  <Header 
    :carrito="carrito"
    :articulo="articulo"
    @decrementar-cantidad="decrementarCantidad"
    @incrementar-cantidad="incrementarCantidad"
    @agregar-carrito="agregarCarrito"
    @eliminar-producto="eliminarProducto"
    @vaciar-carrito="vaciarCarrito"
  />
    <main class="container-xl mt-5">
      <h2 class="text-center">Bienvenidos</h2>

      <div class="row mt-5">
        <Articulo 
              v-for="articulo in articulos"
            :articulo = "articulo" 
            @agregar-carrito="agregarCarrito"
          />
          </div>
    </main>
  </body>
    <Footer/>
  
</template>

<style scoped>
  body{
    background: rgb(116, 221, 190);
  }
  h1{
    text-transform: uppercase;
    color: rgb(13, 6, 54);
  }

</style>
