<script setup>
    import imgCerrarModal from '../assets/img/cerrar.svg'

    const emit = defineEmits(['ocultar-modal'])
    const props = defineProps({
        modal: {
            type: Object,
            required: true
        },
        nombre: {
            type: String,
            required: true
        },
        cantidad: {
            type: [String, Number],
            required: true
        },
        categoria: {
            type: String,
            required: true
        }
    })
</script>

<template>
  <div class="modal">
    <div class="cerrar-modal">
        <img
            :src="imgCerrarModal"
            @click="$emit('ocultar-modal')"
        />
    </div>
    <div 
        class="contenedor contenedor-formulario"
        :class="[modal.animar ? 'animar' : 'cerrar']"
    >
    <form
        class="nuevo-gasto"
    >
        <legend>Añadir Gasto</legend>
        <div class="campo">
            <label for="nombre">Nombre</label>
            <input
                type="text"
                id="nombre"
                placeholder="Añade el nombre del Gasto"
                :value="nombre"
            >
        </div>
        <div class="campo">
            <label for="cantidad">Cantidad</label>
            <input
                type="number"
                id="cantidad"
                placeholder="Añade una cantidad"
                :value="cantidad"
            >
        </div>
        <div class="campo">
            <label for="categoria">Categoría</label>
            <select name="categoria"
                id="categoria"
                :value="categoria"
            >
                <option value="0">[Seleccione]</option>
                <option value="1">Ahorro</option>
                <option value="2">Comida</option>
                <option value="3">Casa</option>
                <option value="4">Gastos varios</option>
                <option value="5">Ocio</option>
                <option value="6">Salud</option>
                <option value="7">Suscripciones</option>
            </select>
        </div>

        <input
            type="submit"
            value="Añadir Gasto"
        >

    </form>

    </div>
  </div>
</template>

<style>
    .modal {
        position: absolute;
        background-color: rgb(0 0 0 / 0.9);
        top: 0;
        bottom: 0;
        right: 0;
        left: 0;
    }
    .cerrar-modal {
        position: absolute;
        right: 3rem;
        top: 3rem;
    }
    .cerrar-modal img {
        width: 3rem;
        cursor: pointer;
    }
    .cerrar-modal img:hover {
        transition: transform 0.2s ease-in-out;
        transform: scale(1.3);
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
    .nuevo-gasto{
        margin: 10rem auto 0 auto;
        display: grid;
        gap: 2rem;
    }
    .nuevo-gasto legend {
        text-align: center;
        color: var(--blanco);
        font-size: 3rem;
        font-weight: 700;
    }
    .campo{
        display: grid;
        gap: 2rem;
    }
    .nuevo-gasto input,
    .nuevo-gasto select {
        background-color: var(--gris-claro);
        border-radius: 1rem;
        padding: 1rem;
        border: none;
        font-size: 2.2rem;
    }
    .nuevo-gasto label {
        color: var(--blanco);
        font-size: 3rem;
    }
    .nuevo-gasto input[type="submit"] {
        background-color: var(--azul);
        color: var(--blanco);
        text-align: center;
        font-weight: 700;
        cursor: pointer;
    }
</style>