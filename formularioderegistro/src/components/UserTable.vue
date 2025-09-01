<template>
  <div class="table-responsive">
    <table class="table table-hover align-middle">
      <thead class="table-dark">
        <tr>
          <th>Nombre</th>
          <th>Correo electrónico</th>
          <th>Edad</th>
        </tr>
      </thead>

      <TransitionGroup name="list" tag="tbody">
        <tr v-for="(u, idx) in users" :key="u.email + '-' + idx">
          <td>{{ u.nombre }}</td>
          <td>
            <a :href="`mailto:${u.email}`">{{ u.email }}</a>
          </td>
          <td><span class="badge bg-primary">{{ u.edad }}</span></td>
        </tr>
      </TransitionGroup>
    </table>
  </div>
</template>

<script setup>
defineProps({
  users: { type: Array, required: true }
});
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
