<template>
    <div class="container d-flex justify-content-center my-5">
        <div class="col-4">
            <select @change="seleccionarCiudad" class="form-select my-5" aria-label="Default select example">
                <option selected>Selecciona una ciudad...</option>
                <option
                    v-for="ciudad in ciudades"
                    :key="ciudad.id"
                    :value="ciudad.nombre"
                >
                    {{ ciudad.nombre }}
                </option>
            </select>
        </div>
    </div>
</template>

<script setup>
    defineProps({
        ciudades: Array
    })

    const emit = defineEmits(['seleccionar'])
    const seleccionarCiudad = (event) => {
        emit('seleccionar', event.target.value)
    }
</script>