<script setup>
    import imgCerrarModal from '../assets/img/cerrar.svg'

    const emit = defineEmits(['ocultar-modal'])
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
        class="contenedor"
    >
    <form>
        <legend>Añadir Gasto</legend>
        <div class="campo">
            <label for="nombre">Nombre</label>
            <input
                type="text"
                id="nombre"
                placeholder="Añade el nombre del Gasto"
            >
        </div>
        <div class="campo">
            <label for="cantidad">Cantidad</label>
            <input
                type="number"
                id="cantidad"
                placeholder="Añade una cantidad"
            >
        </div>
        <div class="campo">
            <label for="categoria">Categoría</label>
            <select name="categoria" id="categoria">
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
</style>