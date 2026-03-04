<template>
    <div class="container d-flex justify-content-center my-5">
        <div class="col-4">
            <div class="card mb-5 p-0">
                <div class="card-header">
                    {{ ciudad }}
                </div>
                <ul class="list-group list-group-flush">
                    <li class="list-group-item">Hoy: {{ hoy }}</li>
                    <li class="list-group-item">Mañana: {{ manana }}</li>
                </ul>
            </div>
        </div>
    </div>
</template>

<script setup>
    defineProps({
        ciudad: String,
        hoy: String,
        manana: String
    })
</script>

<style scoped>
</style>