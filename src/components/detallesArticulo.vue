<template>
  <h5 class="bg-primary text-white q-pa-md q-mb-sm row items-center justify-between">
    Detalles artículo <q-icon name="image" class="q-mr-sm" />
  </h5>
  <div class="row q-gutter-md q-mb-sm">
    <q-input label="Cod.Art.Prov." class="col-2 q-ml-xl" v-model="codArtProv" dense readonly />
    <q-input label="Grupo Talla" class="col-2 q-ml-lg" v-model="talla" dense readonly />
    <q-input label="Família" class="col-2 q-ml-lg" v-model="familia" dense readonly />
    <q-input label="Sección" class="col-3 q-ml-lg" v-model="seccion" dense readonly />
    <q-input label="Temporada" class="col-3 q-ml-xl" v-model="temporada" dense readonly />
    <q-input label="Proveedor" class="col-3 q-ml-lg" v-model="proveedor" dense readonly />
    <q-input label="Nombre" class="col-4 q-ml-lg" v-model="nombre" dense readonly />
    <q-select label="Colores" class="col-3 q-ml-xl" dense />
    <q-input
      label="Precio compra"
      class="col-2 q-ml-lg"
      input-class="text-center"
      v-model="precioCompra"
      dense
    >
      <template v-slot:append>
        <q-icon name="euro" />
      </template>
    </q-input>
    <q-btn outline color="primary" label="NACIONAL" />
    <q-btn outline color="primary" label="IMPORTACIÓN" />
    <q-input
      label="Precio venta"
      class="col-2 q-ml-xl"
      input-class="text-center"
      v-model="precioVenta"
      dense
    >
      <template v-slot:append>
        <q-icon name="euro" />
      </template>
    </q-input>
  </div>
  <q-table
    table-header-class="bg-secondary"
    bordered
    hide-bottom
    dense
    :rows="rows"
    :columns="columns"
    :rows-per-page-options="[0]"
  >
    <!-- Fila totals -->
    <template v-slot:bottom-row>
      <q-tr>
        <q-td></q-td>
        <q-td>{{ totalTu }}</q-td>
        <q-td>{{ totalTotal }}</q-td>
      </q-tr>
    </template>
  </q-table>
  <p class="bg-primary text-white q-pa-sm text-xl text-bold">Últimas recepciones</p>
</template>

<script setup>
import { ref, computed } from 'vue'

const codArtProv = ref(10116)
const talla = ref('UNICA')
const familia = ref('SHORT')
const seccion = ref('ROPA')
const temporada = ref('PRIMAVERA 23')
const proveedor = ref('PROVE1828')
const nombre = ref('SHORT FLUID')
const precioCompra = ref('3,70')
const precioVenta = ref('12,99')

const columns = ref([
  { name: 'color', label: 'Color', field: 'color', align: 'left' },
  { name: 'tu', label: 'TU', field: 'tu', align: 'left' },
  { name: 'total', label: 'Total', field: 'total', align: 'left' },
])

const rows = ref([
  { color: 'AGATA', tu: 1, total: 1 },
  { color: 'BEIX', tu: 1, total: 1 },
  { color: 'BLANC', tu: 1, total: 1 },
  { color: 'BLAU', tu: 2, total: 2 },
  { color: 'BLAU MARI', tu: 4, total: 4 },
  { color: 'GRIS', tu: 3, total: 3 },
  { color: 'CAMEL', tu: 4, total: 4 },
  { color: 'LILA', tu: 6, total: 6 },
])

// Cálculo de totales
const totalTu = computed(() => rows.value.reduce((sum, row) => sum + (row.tu || 0), 0))
const totalTotal = computed(() => rows.value.reduce((sum, row) => sum + (row.total || 0), 0))
</script>
