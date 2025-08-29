<template>
  <div class="table-responsive">
    <table class="table table-hover align-middle">
      <thead class="table-dark">
        <tr>
          <th>Nombre</th>
          <th>Apellido</th>
          <th>Fecha de Nacimiento</th>
          <th>Edad</th>
        </tr>
      </thead>

      <TransitionGroup name="list" tag="tbody">
        <tr v-for="(u, idx) in users" :key="u.nombre + u.apellido + u.fechaNacimiento + '-' + idx">
          <td>{{ u.nombre }}</td>
          <td>{{ u.apellido }}</td>
          <td>{{ formatearFecha(u.fechaNacimiento) }}</td>
          <td><span class="badge bg-primary">{{ calcularEdadFromLocal(u.fechaNacimiento) }}</span></td>
        </tr>
      </TransitionGroup>
    </table>
  </div>
</template>

<script setup>
const props = defineProps({
  users: { type: Array, required: true }
});

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

function formatearFecha(yyyyMmDd) {
  const d = parseLocalDate(yyyyMmDd);
  if (!d) return '';
  return d.toLocaleDateString('es-CL', { year: 'numeric', month: '2-digit', day: '2-digit' });
}
</script>

<style scoped>
.list-enter-active {
  transition: all 280ms ease;
}
.list-enter-from {
  opacity: 0;
  transform: translateY(-6px);
}
</style>
