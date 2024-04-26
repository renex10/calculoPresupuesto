<script setup lang="ts">
import imagen from "@/assets/img/grafico.png"; // Asegúrate de que la ruta de la imagen sea correcta\
import { formatearCantidad } from "@/helpers";
import { defineProps } from 'vue';
const props = defineProps({
    presupuesto: {
        type: Number,
        required: true
    },
    disponible:{
        type: Number,
        required: true

    }
    
});
</script>
<template>
  <div class="dos-columnas">
    <div class="contenedor-grafico">
      <!---renderizado de la imagen-->
      <img :src="imagen" />
    </div>
    <div class="contenedor-presupuesto">
      <button class="reset-app">Resetear presupuesto</button>

      <p>
        <span>presupuesto</span>
        {{formatearCantidad (presupuesto) }}
      </p>
      <p>
        <span>Disponible</span>
        {{formatearCantidad(disponible) }}
      </p>

      <p>
        <span>gastado</span>
        $0
      </p>
    </div>
  </div>
</template>

<style lang="css" scoped>
.dos-columnas {
  display: flex;
  flex-direction: column;
}
.contenedor-grafico {
  display: flex;
  align-items: center;
  justify-content: center; /* Centra el contenido horizontalmente también */
  width: fit-content; /* Ajusta el ancho para que se ajuste al contenido */
}
img {
  width: 40%;
}

.reset-app{
    display: inline-block;
  background-color: #E6E6E6;
  padding: .5em 1em;
  color: #444;
  font-family: inherit;
  font-size: 100%;
  text-align: center;
  text-decoration: none;
  white-space: nowrap;
  cursor: pointer;
  border: 1px solid #999;
  border: transparent;
  border-radius: 2px;
  margin: 3px;
  -webkit-user-drag: none;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}

.reset-app-foco,
.reset-app:focus,
.reset-app:hover {
  filter: alpha(opacity=90);
  background-image: -webkit-linear-gradient(transparent, rgba(0,0,0,.05) 40%, rgba(0,0,0,.1));
  background-image: linear-gradient(transparent, rgba(0,0,0,.05) 40%, rgba(0,0,0,.1));
}

.reset-app-activo,
.reset-app:active {
  box-shadow: 0 0 0 1px rgba(0,0,0,.15) inset, 0 0 6px rgba(0,0,0,.2) inset;
  border-color: #000;
}

.contenedor-presupuesto{
    width: 100%;

}
.contenedor-presupuesto p{
    font-size: 2.4rem;
    text-align: center;
    color:  #4c4e4c ;
}
.contenedor-presupuesto span{
    font-weight: 900;
    color: var(--azul);
    
}

@media (min-width: 760px) {
  .dos-columnas {
    flex-direction: row;
    gap: 4rem;
  }
  .dos-columnas > :first-child {
    margin-bottom: 2rem;
    padding-right: 2rem;
  }
  .dos-columnas > :first-child {
    margin-bottom: 0;
   
  }
  .contenedor-presupuesto p{
    text-align: left;
  }
}


</style>
