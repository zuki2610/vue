<template>
  <div class="form-controls-demo">
    <div class="card mb-4">
      <div class="card-header">
        <h5 class="mb-0">Sección estudios y nacionalidad</h5>
      </div>
      <div class="card-body">
        
        <!-- Sección de Radio Buttons -->
        <section class="mb-4">
          <h6 class="text-primary mb-3">
            <i class="bi bi-radioactive"></i> 
            Controles Radio - Tipo de Estudios
          </h6>
          
          <div class="row">
            <div class="col-md-6">
              <div class="form-group">
                <label class="form-label fw-semibold">Selecciona tu nivel de estudios:</label>
                
                <div class="radio-group">
                  <div class="form-check mb-2">
                    <input 
                      class="form-check-input" 
                      type="radio" 
                      v-model="estudios" 
                      value="primarios" 
                      id="primarios"
                    >
                    <label class="form-check-label" for="primarios">
                      📚 Primarios
                    </label>
                  </div>
                  
                  <div class="form-check mb-2">
                    <input 
                      class="form-check-input" 
                      type="radio" 
                      v-model="estudios" 
                      value="secundarios" 
                      id="secundarios"
                    >
                    <label class="form-check-label" for="secundarios">
                      🎓 Secundarios
                    </label>
                  </div>
                  
                  <div class="form-check mb-2">
                    <input 
                      class="form-check-input" 
                      type="radio" 
                      v-model="estudios" 
                      value="universitarios" 
                      id="universitarios"
                    >
                    <label class="form-check-label" for="universitarios">
                      🎓 Universitarios
                    </label>
                  </div>
                  
                  <div class="form-check mb-2">
                    <input 
                      class="form-check-input" 
                      type="radio" 
                      v-model="estudios" 
                      value="postgrado" 
                      id="postgrado"
                    >
                    <label class="form-check-label" for="postgrado">
                      🎓 Postgrado
                    </label>
                  </div>
                </div>
              </div>
            </div>
            
            <div class="col-md-6">
              <div class="alert alert-info">
                <h6 class="alert-heading">
                  <i class="bi bi-info-circle"></i> 
                  Estado Actual
                </h6>
                <p class="mb-0">
                  <strong>Estudios seleccionados:</strong> 
                  <span class="badge bg-primary ms-2">{{ estudios || 'Ninguno' }}</span>
                </p>
                <small class="text-muted">
                
                </small>
              </div>
            </div>
          </div>
        </section>

        <hr class="my-4">

        <!-- Sección de Select -->
        <section>
          <h6 class="text-success mb-3">
            <i class="bi bi-list-ul"></i> 
            Control Select - País de Residencia
          </h6>
          
          <div class="row">
            <div class="col-md-6">
              <div class="form-group">
                <label class="form-label fw-semibold">Selecciona tu país:</label>
                
                <select 
                  v-model="pais" 
                  class="form-select"
                  :class="{ 'is-invalid': !pais }"
                >
                  <option value="" disabled>
                    🌍 -- Selecciona tu país --
                  </option>
                  <option value="argentina">🇦🇷 Argentina</option>
                  <option value="chile">🇨🇱 Chile</option>
                  <option value="colombia">🇨🇴 Colombia</option>
                  <option value="mexico">🇲🇽 México</option>
                  <option value="peru">🇵🇪 Perú</option>
                  <option value="españa">🇪🇸 España</option>
                  <option value="venezuela">🇻🇪 Venezuela</option>
                  <option value="uruguay">🇺🇾 Uruguay</option>
                  <option value="otro">🌎 Otro</option>
                </select>
                
                <div class="invalid-feedback">
                  Por favor selecciona un país
                </div>
              </div>
            </div>
            
            <div class="col-md-6">
              <div class="alert alert-success">
                <h6 class="alert-heading">
                  <i class="bi bi-check-circle"></i> 
                  Estado Actual
                </h6>
                <p class="mb-0">
                  <strong>País seleccionado:</strong> 
                  <span class="badge bg-success ms-2">{{ pais || 'Ninguno' }}</span>
                </p>
                <small class="text-muted">
            
                </small>
              </div>
            </div>
          </div>
        </section>

        <!-- Resumen Final -->
        <div class="mt-4 p-3 bg-light rounded">
          <h6 class="text-dark mb-2">
            <i class="bi bi-clipboard-data"></i> 
            Tus selecciones
          </h6>
          <div class="row">
            <div class="col-md-6">
              <p class="mb-1"><strong>Estudios:</strong> {{ estudios || 'No seleccionado' }}</p>
            </div>
            <div class="col-md-6">
              <p class="mb-1"><strong>País:</strong> {{ pais || 'No seleccionado' }}</p>
            </div>
          </div>
        </div>

      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'


const estudios = ref('universitarios') 


const pais = ref('') 
</script>

<style scoped>
.form-controls-demo {
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
}

.radio-group {
  background: #f8f9fa;
  padding: 1rem;
  border-radius: 0.5rem;
  border: 1px solid #e9ecef;
}

.form-check-input:checked {
  background-color: #0d6efd;
  border-color: #0d6efd;
}

.form-check-label {
  cursor: pointer;
  font-weight: 500;
  transition: color 0.2s ease;
}

.form-check-label:hover {
  color: #0d6efd;
}

.form-select {
  transition: border-color 0.15s ease-in-out, box-shadow 0.15s ease-in-out;
}

.form-select:focus {
  border-color: #86b7fe;
  box-shadow: 0 0 0 0.25rem rgba(13, 110, 253, 0.25);
}

.alert {
  border: none;
  border-radius: 0.5rem;
}

.card {
  border: none;
  box-shadow: 0 0.125rem 0.25rem rgba(0, 0, 0, 0.075);
}

.card-header {
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  color: white;
  border-radius: 0.5rem 0.5rem 0 0 !important;
}

.badge {
  font-size: 0.875em;
}

code {
  background: #f1f3f4;
  padding: 0.2rem 0.4rem;
  border-radius: 0.25rem;
  font-size: 0.875em;
}

/* Animaciones suaves */
.form-check-input,
.form-select {
  transition: all 0.2s ease;
}

/* Responsive */
@media (max-width: 768px) {
  .radio-group {
    padding: 0.75rem;
  }
  
  .alert {
    margin-top: 1rem;
  }
}
</style>
