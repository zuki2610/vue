# 🎯 Controles Radio y Select en Vue.js

## 📋 Descripción

Este proyecto demuestra cómo implementar correctamente controles de tipo **radio** y **select** en Vue.js, siguiendo las mejores prácticas para el manejo de datos reactivos.

## 🎓 Controles Radio - Tipo de Estudios

### ✅ Implementación Correcta

```vue
<script setup>
import { ref } from 'vue'

// IMPORTANTE: Inicializar con un valor por defecto
const estudios = ref('universitarios') // Valor inicial seleccionado
</script>

<template>
  <div class="form-check">
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
  
  <div class="form-check">
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
</template>
```

### ❌ Implementación Incorrecta

```vue
<!-- NO hagas esto -->
<input checked type="radio" value="universitarios" v-model="estudios" id="universitarios">
```

**Problema:** Vue no rescata automáticamente el atributo `checked` del HTML. Debes inicializar el modelo de datos.

### 🔑 Puntos Clave

1. **Una sola propiedad** en el modelo de datos para todo el grupo de radio
2. **Inicializar el modelo** con el valor por defecto deseado
3. **Mismo `v-model`** para todos los radio buttons del grupo
4. **Valores únicos** en el atributo `value` de cada opción

## 🌍 Control Select - País de Residencia

### ✅ Implementación Correcta

```vue
<script setup>
import { ref } from 'vue'

// IMPORTANTE: Inicializar vacío para forzar selección
const pais = ref('') // Valor inicial vacío
</script>

<template>
  <select v-model="pais" class="form-select">
    <option value="" disabled>
      🌍 -- Selecciona tu país --
    </option>
    <option value="argentina">🇦🇷 Argentina</option>
    <option value="chile">🇨🇱 Chile</option>
    <option value="colombia">🇨🇴 Colombia</option>
  </select>
</template>
```

### 🔑 Puntos Clave

1. **Primera opción deshabilitada** para guiar al usuario
2. **Valor vacío** en la opción placeholder
3. **Inicializar el modelo vacío** para forzar selección
4. **Validación visual** con clases de Bootstrap

## 🎨 Características del Diseño

### ✨ Elementos Visuales

- **Iconos emoji** para hacer la interfaz más amigable
- **Gradientes** en los headers de las tarjetas
- **Colores temáticos** (azul para radio, verde para select)
- **Animaciones suaves** en las transiciones
- **Diseño responsivo** que se adapta a móviles

### 📱 Responsive Design

- **Grid de Bootstrap** para distribución automática
- **Breakpoints** que reorganizan el contenido en móviles
- **Espaciado adaptativo** según el tamaño de pantalla

## 🚀 Cómo Ejecutar

1. Navega al directorio del proyecto:
   ```bash
   cd vue/formularioderegistro
   ```

2. Instala las dependencias:
   ```bash
   npm install
   ```

3. Ejecuta el servidor de desarrollo:
   ```bash
   npm run dev
   ```

4. Abre tu navegador en la URL mostrada (generalmente `http://localhost:5173`)

## 📊 Funcionalidades Demostradas

### 🎯 Controles Radio
- ✅ Selección única entre múltiples opciones
- ✅ Valor inicial predefinido en el modelo
- ✅ Visualización en tiempo real del valor seleccionado
- ✅ Interfaz intuitiva con iconos y colores

### 🎯 Control Select
- ✅ Primera opción deshabilitada como placeholder
- ✅ Validación visual del estado
- ✅ Lista de países con banderas
- ✅ Feedback inmediato de la selección

### 🎯 Características Generales
- ✅ **Reactividad completa** - Los cambios se reflejan inmediatamente
- ✅ **Modelo de datos centralizado** - Un solo lugar para cada tipo de control
- ✅ **Interfaz moderna** - Diseño atractivo y profesional
- ✅ **Documentación en vivo** - Muestra el estado actual del modelo

## 🎓 Conceptos de Vue.js Aplicados

1. **`v-model`** - Enlace bidireccional de datos
2. **`ref()`** - Reactividad para valores primitivos
3. **Computed properties** - Para validaciones y estados derivados
4. **Event handling** - Para interacciones del usuario
5. **Component composition** - Separación de responsabilidades

## 🔧 Estructura del Proyecto

```
src/
├── components/
│   ├── FormControls.vue    # 🆕 Nuevo componente con radio y select
│   ├── UserForm.vue        # Formulario existente
│   └── UserTable.vue       # Tabla de usuarios
├── App.vue                 # Componente principal (actualizado)
└── main.js                 # Punto de entrada
```

## 💡 Próximos Pasos

- Integrar estos controles al formulario principal de usuarios
- Agregar validaciones más avanzadas
- Implementar persistencia de datos
- Crear más tipos de controles (checkbox, textarea, etc.)

---

*¡Disfruta explorando los controles de formulario en Vue.js! 🚀*
