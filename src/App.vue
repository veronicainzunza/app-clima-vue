<template>
  <AppNavbar />
  <SelectCiudades
    :ciudades="ciudades"
    @seleccionar="cargarClima"
  />
  <div v-if="clima">
    <Card
      :ciudad="clima.ciudad"
      :hoy="clima.hoy"
      :manana="clima.manana"
    />
  </div>
</template>

<script setup>
  import { ref } from 'vue'
  import AppNavbar from './components/AppNavbar.vue';
  import SelectCiudades from './components/selectCiudades.vue';
  import Card from './components/Card.vue'
  import dataCiudades from './data/ciudades.json'

  const ciudades = ref(dataCiudades)
  const clima = ref(null)

  const buscarCoordenadas = async (nombreCiudad) => {
    const url = `https://geocoding-api.open-meteo.com/v1/search?name=${nombreCiudad}&country_Code=CL&count=1`
    const response = await fetch(url)
    const data = await response.json()
    console.log(data)
    return {
      lat: data.results[0].latitude,
      lon: data.results[0].longitude
    }
  }

  const cargarClima = async (nombreCiudad) => {
    const coordenadas = await buscarCoordenadas(nombreCiudad)
    const url = `https://api.open-meteo.com/v1/forecast?latitude=${coordenadas.lat}&longitude=${coordenadas.lon}&daily=temperature_2m_max`

    const response = await fetch(url)
    const data = await response.json()

    clima.value = {
      ciudad: nombreCiudad,
      hoy: data.daily.temperature_2m_max[0],
      manana: data.daily.temperature_2m_max[1]
    }
  }

</script>


