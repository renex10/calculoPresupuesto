<script setup lang="ts">
import { ref, reactive } from "vue";
import Prosupuesto from "./components/Prosupuesto.vue";
import ControlPresupuesto from "./components/ControlPresupuesto.vue";
import iconNuevoGasto from "@/assets/img/add.svg" ;
import Modal from "./components/Modal.vue";
//ventana modal
const modal = reactive({
  mostrar:false,
  animar:false,//tendra una animancion
})
//state de gasto
const gasto = reactive({
  nombre:"",
  cantidad:"",
  categoria:"",
  id: null,
  fecha:Date.now//fecha en que se realiza el gasto
  //->pasar todo al formulario

});

// Segundo presupuesto
const presupuesto = ref(0);
//disponible
const disponible = ref(0);

// Definir función para definir el presupuesto con una cantidad
const definirPresupuesto = (cantidad: number) => {
  presupuesto.value = cantidad;
  disponible.value = cantidad;
};

const mostrarModal = () => {
  // Modificar modal
  modal.mostrar = true;
  setTimeout(()=>{
    modal.animar = true;

  },300)

};
//quiero cerrar el Modal  2.0
//animacion 2.0
const ocultarModal = () => {
  // Modificar modal

  modal.animar = false;
  setTimeout(()=>{
    modal.mostrar = false;

  },300)
};

const guardarGastos =()=>{
    console.log('desde app.vue')
    console.log(gasto);
    
  }

</script>



<template>
  <div>
    <header>
    <h1>Planificación de gastos</h1>
    <div class="contenedor-header contenedor sombra">
        <!-- Muestra el componente Prosupuesto si el presupuesto es cero -->
        <Prosupuesto
          v-if="presupuesto === 0"
          @definirPresupuesto ="definirPresupuesto"

        />

        <ControlPresupuesto v-else
        
        :presupuesto="presupuesto"
        :disponible="disponible" />
        
    </div>
</header>
<main  v-if="presupuesto > 0">
  <div class="crear-gasto">


  <!--renderizando iconNuevoGasto -->
  <!----->
<img
:src="iconNuevoGasto"  
alt="icono nuevo gasto"
@click="mostrarModal"

>
</div>
<!----2.1 @ocultar-modal="ocultarModal"-->
<!----3.1 pasando info actualizaciones pasen al componente"-->
<Modal
v-if="modal.mostrar"
@ocultar-modal="ocultarModal"
@guardar-gastos="guardarGastos"
:modal="modal"
v-model:nombre="gasto.nombre"
v-model:cantidad="gasto.cantidad"
v-model:categoria="gasto.categoria"
/>
</main>



    <!---Renderizando el filtro-->
    <Filtro />
  </div>
</template>

<style>
/*agregando estilos globales */
:root {
  --azul: #051e98;
  --negro: #6b6969;
  --blanco: #f3ebf2;
  --gris-claro: #ecf5e8;
  --gris-oscuro: #333333;
  --header: #596355;
}
html {
  font-size: 62.5%;
  box-sizing: border-box;
}
*,
*:before,
*::after {
  box-sizing: inherit;
}

body {
  font-size: 1.6rem;
  font-family: "Arial", sans-serif;
  background-color: var(--gris-claro);
}
h1 {
  font-size: 4rem;
}
h2 {
  font-size: 3.2rem;
}
header {
  background: #00b4db; /* fallback for old browsers */
  background: -webkit-linear-gradient(
    to right,
    #0083b0,
    #00b4db
  ); /* Chrome 10-25, Safari 5.1-6 */
  background: linear-gradient(
    to right,
    #0083b0,
    #00b4db
  ); /* W3C, IE 10+/ Edge, Firefox 16+, Chrome 26+, Opera 12+, Safari 7+ */

  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.8); /* sombra en la parte inferior */
}
header h1 {
  padding: 3rem 0;
  margin: 0;
  color: var(--blanco);
  text-align: center;
}
.contenedor {
  width: 90%;
  max-width: 80rem;
  margin: 0 auto;
}
.contenedor-header {
  margin-top: -5rem;
  transform: translateY(5rem);
  padding: 5rem;
}
.sombra {
  -webkit-box-shadow: 10px 10px 14px -3px rgba(0, 0, 0, 0.35);
  -moz-box-shadow: 10px 10px 14px -3px rgba(0, 0, 0, 0.35);
  box-shadow: 10px 10px 14px -3px rgba(0, 0, 0, 0.35);
  background-color: var(--blanco);
  border-radius: 1.2rem;
  padding: 5rem;
}

/*imagen crear gasto*/
.crear-gasto{
  position: fixed;
  bottom: 5rem;
  right: 5rem;

}
.crear-gasto img {
  width: 5rem;
  cursor: pointer;
}

.crear-gasto img:hover{
  
}
</style>
