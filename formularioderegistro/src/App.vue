<template>
  <div class="container py-4">
    <header class="mb-4">
      <h1 class="text-white display-6">Formulario de Inscripción</h1>
      <p class="text-white d mb-0">
       Usuarios Inscritos 
      </p>
    </header>


    <section class="card shadow-sm mb-4">
      <div class="card-body">
        <FormControls />
      </div>
    </section>

    <section class="card shadow-sm mb-4">
      <div class="card-body">
        <UserForm @add-user="addUser" />
        <div class="d-flex gap-2 mt-3">
          <button class="btn btn-outline-secondary btn-sm" @click="recargarDesdeJSON">
            Restaurar 
          </button>
          <button class="btn btn-outline-danger btn-sm" @click="limpiarTodo">
            Borrar todo
          </button>
        </div>
      </div>
    </section>

    <section class="card shadow-sm">
      <div class="card-header bg-light">
        <strong>Usuarios ({{ users.length }})</strong>
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
import FormControls from './components/FormControls.vue';

const LS_KEY = 'vue-users-demo-v2';
const users = ref([]);

async function inicializar() {
  // 1) localStorage
  try {
    const raw = localStorage.getItem(LS_KEY);
    if (raw) {
      const parsed = JSON.parse(raw);
      if (Array.isArray(parsed) && parsed.length) {
        users.value = parsed;
        return;
      }
    }
  } catch (_) {
  
  }

 
  try {
    const mod = await import('./assets/users.json');
    const baseUsers = (mod?.default ?? mod);
    if (Array.isArray(baseUsers) && baseUsers.length) {
      users.value = baseUsers;
      guardar();
      return;
    }
  } catch (_) {
    
  }

 
  try {
    const res = await fetch('/users.json');
    if (res.ok) {
      const baseUsers = await res.json();
      if (Array.isArray(baseUsers) && baseUsers.length) {
        users.value = baseUsers;
        guardar();
        return;
      }
    }
  } catch (_) {
 
  }

 
  users.value = [];
  guardar();
}

function guardar() {
  localStorage.setItem(LS_KEY, JSON.stringify(users.value));
}

function addUser(user) {
  users.value.unshift({
    nombre: (user.nombre || '').trim(),
    email: (user.email || '').trim(),
    edad: Number(user.edad) || 0,
  });
  guardar();
}

async function recargarDesdeJSON() {

  localStorage.removeItem(LS_KEY);
  await inicializar();
}

function limpiarTodo() {
  users.value = [];
  guardar();
}

onMounted(inicializar);
watch(users, guardar, { deep: true });
</script>

<style>
body { background: #04534a; }
</style>
