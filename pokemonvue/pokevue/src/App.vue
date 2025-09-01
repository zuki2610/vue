<template>
  <main class="app">
    <h1>Poke Vue</h1>

    <section
      v-for="p in personajes"
      :key="p.id"
      class="card"
      @click="p.mostrar = !p.mostrar"
    >
      <img :src="p.imagen" :alt="p.nombre" />
      <div class="info">
        <h2 class="nombre">{{ p.nombre }}</h2>
        <p v-if="p.mostrar" class="descripcion">
          {{ p.descripcion }}
        </p>
      </div>
    </section>
  </main>
</template>

<script setup>
import { ref } from 'vue'

const personajes = ref([
  { 
    id: 1, 
    nombre: "Pikachu", 
    descripcion: "Un ratón eléctrico muy popular, mascota de Ash.",
    imagen: "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/25.png",
    mostrar: false 
  },
  { 
    id: 2, 
    nombre: "Kakuna", 
    descripcion: "Un Pokémon capullo que evoluciona en Beedrill.",
    imagen: "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/14.png",
    mostrar: false 
  },
  { 
    id: 3, 
    nombre: "Beedrill", 
    descripcion: "Un Pokémon avispa con aguijones venenosos.",
    imagen: "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/15.png",
    mostrar: false 
  },
  { 
    id: 4, 
    nombre: "Metapod", 
    descripcion: "Pokémon capullo que suele quedarse inmóvil.",
    imagen: "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/11.png",
    mostrar: false 
  },
  { 
    id: 5, 
    nombre: "Rattata", 
    descripcion: "Un roedor veloz y muy común en los caminos.",
    imagen: "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/19.png",
    mostrar: false 
  }
])
</script>

<style scoped>
.app {
  max-width: 800px;
  margin: 0 auto;
  padding: 24px;
  font-family: system-ui, -apple-system, Segoe UI, Roboto, Arial, sans-serif;
}
h1 { margin-bottom: 16px; color: #222; }
.card {
  display: flex;
  gap: 14px;
  align-items: center;
  padding: 14px;
  border: 1px solid #e5e7eb;
  border-radius: 10px;
  background: #fff;
  margin-bottom: 12px;
  cursor: pointer;
  transition: background .2s ease, transform .05s ease;
}
.card:hover { background: #f9fafb; }
.card:active { transform: scale(0.998); }
img {
  width: 80px;
  height: 80px;
  image-rendering: pixelated;
  border-radius: 8px;
  border: 1px solid #e5e7eb;
  background: #f3f4f6;
}
.info { flex: 1; }
.nombre { font-size: 18px; margin: 0; color: #111827; }
.descripcion { margin: 6px 0 0; color: #4b5563; }
</style>
