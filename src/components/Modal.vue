<script lang="ts" setup>
import { defineProps, defineEmits } from "vue";
// Importar componente Alerta
import Alerta from "./Alerta.vue";
import { ref } from "vue";
// Importar imagen desde asset/img
import cerrarModal from "@/assets/img/cerrar.svg";
import { emit } from "process";

const error = ref("");

// Definir emisiones
const emits = defineEmits([
  "ocultar-modal",
  "guardar-gastos",
  "update:nombre",
  "update:cantidad",
  "update:categoria",
]);

// Definir propiedades
const props = defineProps({
  modal: {
    type: Object,
    required: true,
  },
  nombre: {
    type: String,
    required: true,
  },
  cantidad: {
    type: [String, Number],
    required: true,
  },
  categoria: {
    type: String,
    required: true,
  },
});

const agregarGasto = () => {
  // Validar que no hayan campos vacíos
  const { cantidad, categoria, nombre } = props;
  if (!cantidad || !categoria || !nombre) {
    error.value = "Todos los campos son obligatorios";
    // Después de unos segundos, limpiar el error
    setTimeout(() => {
      error.value = "";
    }, 3000);
    return;
  }
  
  // Aquí puedes agregar la lógica adicional para agregar el gasto

  if (cantidad <= 0) {
    error.value = "Cantidad no válida";
    // Después de unos segundos, limpiar el error
    setTimeout(() => {
      error.value = "";
    }, 3000);
    return;
  }

  emits('guardar-gastos'); // Emitir el evento 'guardar-gastos'

};
</script>

<template>
  <div class="modal">
    <div class="cerrar-modal">
      <img :src="cerrarModal" @click="$emit('ocultar-modal')" />
    </div>

    <div
      class="contenedor contenedor-formulario"
      :class="{ animar: modal.animar, cerrar: !modal.mostrar }"
    >
      <form class="nuevo-gasto" @submit.prevent="agregarGasto">
        <legend>Añade Gasto</legend>
        <Alerta v-if="error">{{ error }}</Alerta>
        <div class="campo">
          <label for="nombre">Nombre del gasto</label>
          <input
            type="text"
            id="nombre"
            placeholder="Añade tu gasto"
            :value="nombre"
            @input="$emit('update:nombre', $event.target.value)"
          />
        </div>
        <div class="campo">
          <label for="cantidad">Cantidad</label>
          <input
            type="number"
            id="cantidad"
            placeholder="Añade la cantidad del gasto"
            :value="cantidad"
            @input="$emit('update:cantidad', $event.target.value)"
          />
        </div>
        <div class="campo">
          <label for="categoria">Categoría</label>
          <select
            id="categoria"
            :value="categoria"
            @input="$emit('update:categoria', $event.target.value)"
          >
            <option value="comida">Comida</option>
            <option value="ahorro">Ahorro</option>
            <option value="casa">Casa</option>
            <option value="ocio">Ocio</option>
            <option value="suscripciones">Suscripciones</option>
            <option value="salud">Salud</option>
            <option value="alcohol">Alcohol</option>
          </select>
        </div>
        <input type="submit" value="Añadir Gasto" />
      </form>
    </div>
  </div>
</template>

<style lang="css" scoped>
.modal {
  /*desde toda la pantalla la posicion absoluta,tomara toda la pantalla*/
  position: absolute;
  background-color: rgb(0 0 0 /0.9);
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
}

.cerrar-modal {
  position: absolute;
  right: 3rem;
  top: 3rem;
}

.contenedor-formulario {
  transition-property: all;
  transition-duration: 300ms;
  transition-timing-function: ease-in;
  opacity: 0;
}

.contenedor-formulario.animar {
  opacity: 1;
}
.contenedor-formulario.cerrar {
  opacity: 0;
}

/* Aquí cambiamos .cerrar-modal.img a .cerrar-modal img */
.cerrar-modal img {
  width: 3rem;
  cursor: pointer;
}
.nuevo-gasto {
  margin: 10rem auto 0 auto;
  display: grid;
  gap: 2rem;
}
.nuevo-gasto legend {
  text-align: center;
  color: antiquewhite;
  font-size: 3.5rem;
  font-weight: 700;
}
.campo {
  display: grid;
  gap: 2.2rem;
}
.nuevo-gasto input,
.nuevo-gasto select {
  background: #d3cce3; /* fallback for old browsers */
  background: -webkit-linear-gradient(
    to right,
    #e9e4f0,
    #d3cce3
  ); /* Chrome 10-25, Safari 5.1-6 */
  background: linear-gradient(
    to right,
    #e9e4f0,
    #d3cce3
  ); /* W3C, IE 10+/ Edge, Firefox 16+, Chrome 26+, Opera 12+, Safari 7+ */
  border-radius: 1rem;
  padding: 1rem;
  border: none;
  font-size: 2.3rem;
}
.nuevo-gasto label {
  color: bisque;
  font-weight: bold;
  text-transform: uppercase;
  font-size: 3rem;
}

.nuevo-gasto input[type="submit"] {
  background: #56ab2f; /* fallback for old browsers */
  background: -webkit-linear-gradient(
    to right,
    #a8e063,
    #56ab2f
  ); /* Chrome 10-25, Safari 5.1-6 */
  background: linear-gradient(
    to right,
    #a8e063,
    #56ab2f
  ); /* W3C, IE 10+/ Edge, Firefox 16+, Chrome 26+, Opera 12+, Safari 7+ */
  color: black;
  font-weight: 700;
  cursor: pointer;
}
</style>
