<template>
  <form class="row g-3 align-items-end" @submit.prevent="handleSubmit">
    <div class="col-md-3">
      <label class="form-label">Nombre y Apellido</label>
      <input
        v-model.trim="nombre"
        type="text"
        class="form-control"
        placeholder="Ej: Miguel Rondanelli"
        required
      />
    </div>

    <div class="col-md-3">
      <label class="form-label">Correo electrónico</label>
      <input
        v-model.trim="email"
        type="email"
        class="form-control"
        placeholder="ejemplo@correo.com"
        required
      />
    </div>

    <div class="col-md-2">
      <label class="form-label">Edad</label>
      <input
        v-model.number="edad"
        type="number"
        min="0"
        max="120"
        class="form-control"
        placeholder="Ej: 30"
        required
      />
    </div>

    <div class="col-md-2 d-grid gap-2 d-md-block">
      <button class="btn btn-primary w-100" type="submit">Agregar</button>
      <button class="btn btn-outline-secondary w-100 mt-2" type="button" @click="limpiarFormulario">
        Limpiar formulario
      </button>
    </div>

    <!-- Resumen: solo visible cuando todos los campos están completos -->
    <div class="col-12">
      <div class="alert alert-info mt-2" v-if="isComplete">
        <h6 class="mb-2">Resumen de datos</h6>
        <ul class="mb-0">
          <li><strong>Nombre:</strong> {{ nombre }}</li>
          <li><strong>Correo:</strong> {{ email }}</li>
          <li><strong>Edad:</strong> {{ edad }}</li>
        </ul>
      </div>
    </div>
  </form>
</template>

<script setup>
import { computed, ref } from 'vue';

const emit = defineEmits(['add-user']);

const nombre = ref('');
const email = ref('');
const edad = ref(null);

const isComplete = computed(() =>
  !!nombre.value && !!email.value && Number.isFinite(edad.value)
);

function handleSubmit() {
  if (!isComplete.value) return;
  emit('add-user', {
    nombre: nombre.value,
    email: email.value,
    edad: edad.value
  });
  limpiarFormulario();
}

function limpiarFormulario() {
  nombre.value = '';
  email.value = '';
  edad.value = null;
}
</script>
