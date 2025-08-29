<template>
  <form class="row g-3 align-items-end" @submit.prevent="handleSubmit">
    <div class="col-md-3">
      <label class="form-label">Nombre</label>
      <input
        v-model.trim="nombre"
        type="text"
        class="form-control"
        placeholder="Ej: Miguel"
        required
      />
    </div>

    <div class="col-md-3">
      <label class="form-label">Apellido</label>
      <input
        v-model.trim="apellido"
        type="text"
        class="form-control"
        placeholder="Ej: Rondanelli"
        required
      />
    </div>

    <div class="col-md-2">
      <label class="form-label">Fecha de Nacimiento</label>
      <div class="position-relative">
        <input
          v-model="fechaNacimiento"
          type="date"
          class="form-control"
          required
        />
        <div
          class="form-text position-absolute w-100"
          v-if="fechaNacimiento"
          style="top: 100%; left: 0;"
        >
          Edad estimada: <strong>{{ edadPreview }}</strong>
        </div>
      </div>
    </div>

  
    <div class="col-md-2 d-grid">
      <button class="btn btn-primary" type="submit">
        Agregar usuario
      </button>
    </div>
  </form>
</template>

<script setup>
import { computed, ref } from 'vue';

const emit = defineEmits(['add-user']);

const nombre = ref('');
const apellido = ref('');
const fechaNacimiento = ref('');

function parseLocalDate(yyyyMmDd) {
  if (!yyyyMmDd) return null;
  const [y, m, d] = yyyyMmDd.split('-').map(Number);
  return new Date(y, (m ?? 1) - 1, d ?? 1);
}

function calcularEdadFromLocal(yyyyMmDd) {
  const dob = parseLocalDate(yyyyMmDd);
  if (!dob) return '-';
  const today = new Date();
  let age = today.getFullYear() - dob.getFullYear();
  const m = today.getMonth() - dob.getMonth();
  if (m < 0 || (m === 0 && today.getDate() < dob.getDate())) age--;
  return age;
}

const edadPreview = computed(() =>
  fechaNacimiento.value ? calcularEdadFromLocal(fechaNacimiento.value) : '-'
);

function handleSubmit() {
  if (!nombre.value || !apellido.value || !fechaNacimiento.value) return;

  emit('add-user', {
    nombre: nombre.value,
    apellido: apellido.value,
    fechaNacimiento: fechaNacimiento.value,
  });

  nombre.value = '';
  apellido.value = '';
  fechaNacimiento.value = '';
}
</script>
