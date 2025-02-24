<template>
  <h5 class="bg-primary text-white q-pa-md q-mb-sm row items-center justify-between">
    <div><q-icon name="sell" class="q-mr-sm" /> Fechas rebaja</div>
    <q-checkbox v-model="checkbox" class="" dense />
  </h5>
  <q-select
    label="Buscar artículo"
    class="col-2 q-ml-lg"
    v-model="buscarArticulo"
    :options="articulos"
  >
    <template v-slot:append>
      <q-icon v-if="buscarArticulo !== null" class="cursor-pointer q-mr-md" name="edit" />
      <q-icon
        v-if="buscarArticulo !== null"
        class="cursor-pointer q-mr-sm"
        name="close"
        @click.stop.prevent="buscarArticulo = null"
      />
    </template>
  </q-select>
</template>

<script setup>
import { ref } from 'vue'

const buscarArticulo = ref(null)
const articulos = ['SHORT FLUID', 'CAMISETA']
const checkbox = ref(false)
</script>
