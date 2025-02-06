<template>
  <div id="app">
    <Header 
      :carrito="carrito" 
      @vaciar-carrito="vaciarCarrito"
      @eliminar-item="eliminarItem"
      @aumentar-cantidad="aumentarCantidad"
      @disminuir-cantidad="disminuirCantidad"
    />
    <Libros :libros="libros" @agregar-carrito="agregarAlCarrito" />
    <Footer />
  </div>
</template>

<script>
import Header from './components/AppHeader.vue'
import Libros from './components/AppLibros.vue'
import Footer from './components/AppFooter.vue'
import librosData from './libros.js'

export default {
  components: { Header, Libros, Footer },
  data() {
    return {
      libros: librosData,
      carrito: []
    }
  },
  methods: {
    agregarAlCarrito(libro) {
      const existe = this.carrito.find(item => item.id === libro.id)
      existe ? existe.cantidad++ : this.carrito.push({ ...libro, cantidad: 1 })
    },
    vaciarCarrito() {
      this.carrito = []
    },
    eliminarItem(itemId) {
      this.carrito = this.carrito.filter(item => item.id !== itemId)
    },
    aumentarCantidad(itemId) {
      const item = this.carrito.find(i => i.id === itemId)
      if (item) item.cantidad++
    },
    disminuirCantidad(itemId) {
      const item = this.carrito.find(i => i.id === itemId)
      if (item) item.cantidad > 1 ? item.cantidad-- : this.eliminarItem(itemId)
    }
  }
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: 'Arial', sans-serif;
}

body {
  background-color: #f5f6fa;
  min-height: 100vh;
  display: flex;
  flex-direction: column;
}

#app {
  flex: 1;
  display: flex;
  flex-direction: column;
  padding-bottom: 60px;
}

@media (max-width: 768px) {
  .libros-container {
    grid-template-columns: 1fr;
    padding: 1rem;
  }
}
</style>