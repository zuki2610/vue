<template>
  <div class="container py-4">
    <header class="mb-4">
      <h1 class="text-white display-6">Formulario de Inscripción</h1>
      <p class="text-white mb-0">
     Base de datos inscritos en Formulario
      </p>
    </header>

    <section class="card shadow-sm mb-4">
      <div class="card-body">
        <UserForm @add-user="addUser" />
        <div class="d-flex gap-2 mt-3">
          <button class="btn btn-outline-secondary btn-sm" @click="recargarDesdeJSON">
            Restaurar usuarios base
          </button>
          <button class="btn btn-outline-danger btn-sm" @click="limpiarTodo">
            Limpiar todo
          </button>
        </div>
      </div>
    </section>

    <section class="card shadow-sm">
      <div class="card-header bg-light">
        <strong>Usuarios Inscritos ({{ users.length }})</strong>
      </div>
      <div class="card-body">
        <UserTable :users="users" />
      </div>
    </section>
  </div>
</template>

<script setup>
import { ref, onMounted, watch } from 'vue';
import UserForm from './components/UserForm.vue';
import UserTable from './components/UserTable.vue';
import baseUsers from './assets/users.json';

const LS_KEY = 'vue-users-demo';
const users = ref([]);

function inicializar() {
  try {
    const raw = localStorage.getItem(LS_KEY);
    if (raw) {
      const parsed = JSON.parse(raw);
      users.value = Array.isArray(parsed) ? parsed : [];
      if (!users.value.length) {
        users.value = [...baseUsers];
        guardar();
      }
    } else {
      users.value = [...baseUsers];
      guardar();
    }
  } catch {
    users.value = [...baseUsers];
    guardar();
  }
}

function guardar() {
  localStorage.setItem(LS_KEY, JSON.stringify(users.value));
}


function addUser(user) {

  const fechaStr = String(user.fechaNacimiento).slice(0, 10);
  users.value.unshift({
    nombre: (user.nombre || '').trim(),
    apellido: (user.apellido || '').trim(),
    fechaNacimiento: fechaStr,
  });
  guardar();
}

function recargarDesdeJSON() {
  users.value = [...baseUsers];
  guardar();
}

function limpiarTodo() {
  users.value = [];
  guardar();
}

onMounted(inicializar);
watch(users, guardar, { deep: true });
</script>

<style>
body {
  background: #04534a;
}
</style>
