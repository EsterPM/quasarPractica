<template>
  <h5 class="bg-primary text-white q-pa-md q-mb-sm">Líneas de pedido recibidas</h5>
  <div class="row q-gutter-md q-mb-sm">
    <q-select
      label="Albaranes pedido"
      class="col-2 q-ml-lg"
      v-model="albaranes"
      :options="opcionesAlbaranes"
    >
      <template v-slot:append>
        <q-icon
          v-if="albaranes !== null"
          class="cursor-pointer"
          name="cancel"
          @click.stop.prevent="albaranes = null"
        />
      </template>
    </q-select>
    <q-input label="Fecha albaran pedido" v-model="fechaAlbaranPedido" readonly />
    <q-select label="Centro" class="col-2 q-ml-lg" />
    <q-select label="Empresa" class="col-2 q-ml-lg" />
    <q-select label="Proveedor" class="col-2 q-ml-lg" />
    <q-input label="Código albarán" class="col-2 q-ml-lg" dense />
    <q-btn class="bg-primary text-white">
      <q-icon name="add" class="q-mr-sm" /> NUEVO ALBARÁN
    </q-btn>
    <q-btn class="bg-accent text-white">
      <q-icon name="delete" class="q-mr-sm" /> ELIMINAR ALBARÁN
    </q-btn>
    <q-btn class="bg-primary text-white">
      <q-icon name="print" />
    </q-btn>
    <q-btn class="bg-primary text-white">
      <q-icon name="upload_file" />
    </q-btn>
  </div>

  <q-table
    table-header-class="bg-secondary"
    flat
    bordered
    hide-bottom
    dense
    :rows="rows"
    :columns="columns"
  >
    <!-- Columna de acciones -->
    <template v-slot:body-cell-acciones="props">
      <q-td :props="props">
        <q-icon name="image" class="q-mr-sm" />
        <q-icon name="print" class="q-mr-sm text-primary" />
        <q-icon name="delete" class="q-mr-sm text-accent" />
      </q-td>
    </template>
    <!-- Columna L -->
    <template v-slot:body-cell-l="props">
      <q-td :props="props">
        <q-checkbox v-model="props.row.l" dense />
      </q-td>
    </template>

    <!-- Fila totals -->
    <template v-slot:bottom-row>
      <q-tr class="text-bold">
        <q-td colspan="7" align="right">TOTALS:</q-td>
        <q-td align="right">{{ totalUPedidas }}</q-td>
        <q-td align="right">{{ totalURecibidas }}</q-td>
        <q-td></q-td>
        <q-td align="right">{{ totalGeneral }}</q-td>
        <q-td colspan="2"></q-td>
      </q-tr>
    </template>
  </q-table>
  <div class="row justify-end">
    <q-btn class="bg-primary text-white q-mt-sm q-mr-sm"> CONFIRMAR RECEPCIÓN </q-btn>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'

const albaranes = ref(null)
const opcionesAlbaranes = ['Albaran 1', 'Albaran 2', 'Albaran 3']
const fechaAlbaranPedido = ref('13/12/2024 09:55:19')

const columns = ref([
  { name: 'acciones', label: 'Acciones', field: 'acciones', align: 'left' },
  { name: 'proveedor', label: 'Proveedor', field: 'proveedor', align: 'left' },
  { name: 'codArtProv', label: 'Cod.Art.Prov', field: 'codArtProv', align: 'left' },
  { name: 'etiquetas', label: 'Etiquetas', field: 'etiquetas', align: 'left' },
  { name: 'nombre', label: 'Nombre', field: 'nombre', align: 'left' },
  { name: 'color', label: 'Color', field: 'color', align: 'left' },
  { name: 'talla', label: 'Talla', field: 'talla', align: 'left' },
  { name: 'uPedidas', label: 'U Pedidas', field: 'uPedidas', align: 'right' },
  { name: 'uRecibidas', label: 'U.Recibidas', field: 'uRecibidas', align: 'right' },
  {
    name: 'precioU',
    label: 'Precio U',
    field: (row) => row.precioU.toFixed(2) + ' €',
    align: 'right',
  },
  {
    name: 'total',
    label: 'Total',
    field: (row) => (row.uRecibidas * row.precioU).toFixed(2) + ' €',
    align: 'right',
  },
  { name: 'incidencia', label: 'Incidencia', field: 'incidencia', align: 'left' },
  { name: 'l', label: 'L', field: 'l', align: 'center' },
])

const rows = ref([
  {
    proveedor: 'PROVE1828',
    codArtProv: 10116,
    etiquetas: 'PRIMAVERA 23',
    nombre: 'SHORT FLUID',
    color: 'BLANC',
    talla: 'TU',
    uPedidas: 0,
    uRecibidas: 1,
    precioU: 3.7,
    l: false,
  },
  {
    proveedor: 'PROVE1828',
    codArtProv: 10116,
    etiquetas: 'PRIMAVERA 23',
    nombre: 'SHORT FLUID',
    color: 'BLAU',
    talla: 'TU',
    uPedidas: 0,
    uRecibidas: 2,
    precioU: 3.7,
    l: false,
  },
  {
    proveedor: 'PROVE1828',
    codArtProv: 10116,
    etiquetas: 'PRIMAVERA 23',
    nombre: 'SHORT FLUID',
    color: 'CAMEL',
    talla: 'TU',
    uPedidas: 0,
    uRecibidas: 4,
    precioU: 3.7,
    l: false,
  },
  {
    proveedor: 'PROVE1828',
    codArtProv: 10116,
    etiquetas: 'PRIMAVERA 23',
    nombre: 'SHORT FLUID',
    color: 'BEIX',
    talla: 'TU',
    uPedidas: 0,
    uRecibidas: 6,
    precioU: 3.7,
    l: false,
  },
  {
    proveedor: 'PROVE1828',
    codArtProv: 10116,
    etiquetas: 'PRIMAVERA 23',
    nombre: 'SHORT FLUID',
    color: 'GRIS',
    talla: 'TU',
    uPedidas: 0,
    uRecibidas: 3,
    precioU: 3.7,
    l: false,
  },
])

// Cálculo de totales
const totalUPedidas = computed(() => rows.value.reduce((sum, row) => sum + (row.uPedidas || 0), 0))
const totalURecibidas = computed(() =>
  rows.value.reduce((sum, row) => sum + (row.uRecibidas || 0), 0),
)
const totalGeneral = computed(
  () =>
    rows.value
      .reduce((sum, row) => sum + (row.uRecibidas || 0) * (row.precioU || 0), 0)
      .toFixed(2) + ' €',
)
</script>
