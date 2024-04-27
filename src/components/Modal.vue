<script lang="ts" setup>
//2.2
import { defineEmits } from "vue";
import { defineProps } from "vue";

//importar imagen desde asset/img
import cerrarModal from "@/assets/img/cerrar.svg";
//registrando el emit de la funcion cerrar modal

//2.3
const emits = defineEmits(["ocultar-modal"]);
const props = defineProps({
  modal: {
    type: Object,
    required: true,
  },
});
</script>

<template>
  <!---2.4 @click="$emit('ocultar-modal')"/>-->
  <div class="modal">
    <div class="cerrar-modal">
      <img :src="cerrarModal" @click="$emit('ocultar-modal')" />
    </div>

    <!---agregando contenido al modal-->
    <!---todo el formulario sin action-->
    <div
      class="contenedor contenedor-formulario"
      :class="{ 'animar': modal.animar, 'cerrar': !modal.mostrar }"
    >
      <form class="nuevo-gasto">
        <legend>Añade Gasto</legend>
        <div class="campo">
          <label for="nombre">Nombre del gasto</label>
          <input type="text" id="nombre" placeholder="añade tu gasto" />
        </div>

        <div class="campo">
          <label for="cantidad">Cantidad</label>
          <input
            type="number"
            id="cantidad"
            placeholder="añade la cantidad del gasto. ej.500"
          />
        </div>

        <div class="campo">
          <label for="cantidad">Categoria</label>
          <select name="" id="categoria">
            <option value="comida">comida</option>
            <option value="ahorro">ahorro</option>
            <option value="casa">casa</option>
            <option value="ocio">ocio</option>
            <option value="suscripciones">suscripciones</option>
            <option value="salud">salud</option>
            <option value="alcohol">alcohol</option>
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
