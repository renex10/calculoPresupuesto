<script lang="ts" setup>
import { ref, defineEmits } from "vue";
import Alerta from "./Alerta.vue";

//1 incia en 0
const presupuesto = ref(0);
//imprimiendo el mensaje de error
const error = ref('');

const emit = defineEmits(['definir-presupuesto']);
const definirPresupuesto = () => {
    if (presupuesto.value <= 0 || presupuesto === '') {
        error.value = 'presupuesto no válido';

        //después de unos segundos vuelve
        setTimeout(() => {
            error.value = "";
        }, 3000);
        return
    } 
    emit('definir-presupuesto', presupuesto.value);
}
</script>







<template>
    <form action="" class="presupuesto" @submit.prevent="definirPresupuesto">
        <Alerta 
        v-if="error"
        >
            <!--renderizano el error-->
            {{ error }}
          
        </Alerta><!---permite que un componente sensillo,notengas que pserles props y definirlos-->
        <div class="campo">
            <label for="nuevo-presupuesto">Definir presupuesto</label>
            <input id="nuevo-presupuesto" class="nuevo-presupuesto" placeholder="Agrega tu presupuesto" type="number" min="0" v-model.number="presupuesto">
        </div>
        <input type="submit" value="Definir presupuesto">
    </form>
</template>

<style scoped>
.presupuesto {
    width: 100%;
}

.campo {
    display: grid;
    gap: 2rem;
}
.presupuesto label{
    font-size: 3rem;
    text-align: center;
    color: var(--gris-oscuro);
}

.presupuesto input[type="number"] {
    background-color: var(--gris-claro);
    border-radius: 1.5rem;
    padding: 1.3rem;
    border: none;
    font-size: 2.3rem;
    text-align: center;
}

.presupuesto input[type="submit"]{
    background-color:  var(--azul);
    border: none;
    padding: 1.4rem;
text-align: center ;
font-size: 2.2rem;
color: var(--blanco);
font-weight: 900;
width: 100%;
transition: background-color 300ms ease;
}

.presupuesto input[type="submit"]:hover {
    cursor: pointer;
    background-color: darkslateblue;

}
</style>
