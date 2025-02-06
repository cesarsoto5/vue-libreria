<template>
  <header>
    <h1>Librería Online</h1>
    <button @click="carritoVisible = !carritoVisible" class="boton-carrito">
      🛒 {{ carrito.length }}
    </button>
    
    <div class="carrito" :class="{ 'cerrado': !carritoVisible }">
      <div class="encabezado-carrito">
        <h2>Carrito ({{ carrito.length }})</h2>
        <button @click="carritoVisible = false" class="cerrar-carrito">×</button>
      </div>
      
      <div v-for="item in carrito" :key="item.id" class="item-carrito">
        <img :src="item.imagen" :alt="item.nombre" width="50">
        <div class="info-item">
          <p>{{ item.nombre }}</p>
          <div class="controles-cantidad">
            <button @click="$emit('disminuir-cantidad', item.id)">-</button>
            <span>{{ item.cantidad }}</span>
            <button @click="$emit('aumentar-cantidad', item.id)">+</button>
          </div>
          <p>${{ (item.precio * item.cantidad).toFixed(2) }}</p>
        </div>
        <button class="eliminar-item" @click="$emit('eliminar-item', item.id)">×</button>
      </div>
      
      <h3>Total: ${{ total }}</h3>
      <div class="acciones-carrito">
        <button @click="$emit('vaciar-carrito')">Vaciar Todo</button>
        <button @click="carritoVisible = false">Seguir Comprando</button>
      </div>
    </div>
  </header>
</template>

<script>
export default {
  props: ['carrito'],
  data() {
    return {
      carritoVisible: false
    }
  },
  computed: {
    total() {
      return this.carrito.reduce((sum, item) => sum + (item.precio * item.cantidad), 0).toFixed(2)
    }
  }
}
</script>

<style scoped>
header {
  background-color: #2c3e50;
  color: white;
  padding: 1rem;
  position: relative;
  z-index: 1000;
}

h1 {
  text-align: center;
  font-size: 1.8rem;
}

.boton-carrito {
  background: #42b983;
  color: white;
  border: none;
  padding: 10px 20px;
  border-radius: 25px;
  cursor: pointer;
  position: fixed;
  right: 20px;
  top: 20px;
  z-index: 1001;
  box-shadow: 0 2px 8px rgba(0,0,0,0.2);
  display: flex;
  align-items: center;
  gap: 8px;
}

.carrito {
  background-color: white;
  color: #2c3e50;
  padding: 1rem;
  border-radius: 8px;
  position: fixed;
  right: 20px;
  top: 80px;
  width: 350px;
  max-height: 70vh;
  overflow-y: auto;
  z-index: 1000;
  box-shadow: 0 2px 15px rgba(0,0,0,0.2);
  transition: transform 0.3s ease-in-out;
}

.carrito.cerrado {
  transform: translateX(120%);
}

.item-carrito {
  display: flex;
  gap: 15px;
  margin: 15px 0;
  padding: 10px;
  border-bottom: 1px solid #eee;
  position: relative;
}

.item-carrito img {
  width: 50px;
  height: 70px;
  object-fit: cover;
  border-radius: 4px;
}

.info-item {
  flex-grow: 1;
}

.controles-cantidad {
  display: flex;
  align-items: center;
  gap: 10px;
  margin: 5px 0;
}

.controles-cantidad button {
  padding: 2px 8px;
  background: #42b983;
  border: none;
  border-radius: 4px;
  color: white;
  cursor: pointer;
}

.eliminar-item {
  background: #e74c3c;
  color: white;
  border: none;
  border-radius: 50%;
  width: 24px;
  height: 24px;
  cursor: pointer;
  position: absolute;
  right: 0;
  top: 50%;
  transform: translateY(-50%);
}

.acciones-carrito {
  display: grid;
  gap: 10px;
  margin-top: 1rem;
}

.acciones-carrito button {
  padding: 10px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

.acciones-carrito button:first-child {
  background: #e74c3c;
  color: white;
}

.acciones-carrito button:last-child {
  background: #42b983;
  color: white;
}

@media (max-width: 768px) {
  .carrito {
    width: 90%;
    right: 5%;
    top: 70px;
  }
}
</style>