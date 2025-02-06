<template>
  <main>
    <div class="libros-container">
      <div v-for="libro in libros" :key="libro.id" class="libro">
        <img :src="libro.imagen" :alt="libro.nombre">
        <h3>{{ libro.nombre }}</h3>
        <p class="autor">{{ libro.autor }}</p>
        <p class="precio">${{ libro.precio }}</p>
        <button @click="$emit('agregar-carrito', libro)">Agregar al carrito</button>
      </div>
    </div>
  </main>
</template>

<script>
export default {
  props: ['libros']
}
</script>

<style scoped>
.libros-container {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
  gap: 2rem;
  padding: 2rem;
  max-width: 1200px;
  margin: 0 auto;
}

.libro {
  background: white;
  border-radius: 10px;
  padding: 1.5rem;
  box-shadow: 0 2px 8px rgba(0,0,0,0.1);
  transition: transform 0.3s;
  text-align: center;
}

.libro:hover {
  transform: translateY(-5px);
}

.libro img {
  width: 100%;
  height: 300px;
  object-fit: cover;
  border-radius: 4px;
  margin-bottom: 1rem;
}

.libro h3 {
  color: #2c3e50;
  font-size: 1.1rem;
  margin-bottom: 0.5rem;
}

.autor {
  color: #666;
  font-size: 0.9rem;
  margin-bottom: 0.5rem;
}

.precio {
  color: #42b983;
  font-weight: bold;
  font-size: 1.2rem;
  margin: 1rem 0;
}

button {
  background-color: #42b983;
  color: white;
  border: none;
  padding: 10px 20px;
  border-radius: 4px;
  cursor: pointer;
  width: 100%;
  transition: background-color 0.3s;
}

button:hover {
  background-color: #359c6e;
}
</style>