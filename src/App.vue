<script setup>
  import { ref, reactive } from 'vue'
  import Presupuesto from './components/Presupuesto.vue'
  import ControlPresupuesto from './components/ControlPresupuesto.vue'
  import Modal from './components/Modal.vue'
  import iconoNuevoGasto from './assets/img/nuevo-gasto.svg'

  const modal = reactive({
    mostrar: false,
    animar: false
  })

  const presupuesto = ref(0)
  const disponible = ref(0)

  const gasto = reactive({
    nombre: 'Gasto ejemplo',
    cantidad: '400',
    categoria: '5',
    id: null,
    fecha: Date.now()
  })

  const definirPresupuesto = ((cantidad) => {
    presupuesto.value = cantidad
    disponible.value = cantidad
  })

  const mostrarModal = () => {
    modal.mostrar = true,    
    setTimeout(() => {
      modal.animar = true
    },300)
  }

  const ocultarModal = () => {    
    modal.animar = false
    setTimeout(() => {
      modal.mostrar = false
    }, 300);
  }

</script>

<template>
  <div>
    <header>
      <h1>Planificador de Gastos</h1>

      <div class="contenedor-header contenedor sombra">
        <Presupuesto
          v-if="presupuesto === 0"
          @definir-presupuesto="definirPresupuesto"
        />
        <ControlPresupuesto
          v-else
          :presupuesto="presupuesto"
          :disponible="disponible"
        />

      </div>

    </header>

    <main v-if="presupuesto > 0">
      <div class="crear-gasto">
        <img
          :src="iconoNuevoGasto"
          alt:="Icono nuevo gasto"
          @click="mostrarModal"
        />
      </div>

      <Modal
        v-if="modal.mostrar === true"
        @ocultar-modal="ocultarModal"
        :modal="modal"
        v-model:nombre="gasto.nombre"
        v-model:cantidad="gasto.cantidad"
        v-model:categoria="gasto.categoria"
     />
    </main>

  </div>
</template>

<style>
  :root{
    --azul: #3b82f6;
    --blanco: #FFF;
    --gris-claro: #F5F5F5;
    --gris: #94a3b8;
    --gris-oscuro: #64748b;
    --negro: #000;
  }

  html {
    font-size: 62.5%;
    box-sizing: border-box;
  }
  *,
  *:before,
  *after {
    box-sizing: inherit;
  }
  body{
    font-size: 1.6rem;
    font-family: "Lato", sans-serif;
    background-color: var(--gris-claro);
  }
  h1 {
    font-size: 4rem;
  }
  h2 {
    font-size: 3rem;
  }

  header {
    background-color: var(--azul);
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
    box-shadow: 0px 15px 15px -3px rgba(0,0,0,0.1);
    background-color: var(--blanco);
    border-radius: 1.2rem;
    padding: 5rem;
  }
   .crear-gasto{
    position: fixed;
    bottom: 5rem;
    right: 5rem;
   }
   .crear-gasto img {
    width: 6rem;
    transition: transform 0.3s ease, box-shadow 0.3s ease;
   }
   .crear-gasto img:hover {
    cursor: pointer;
    transform: scale(1.2);
  }

</style>
