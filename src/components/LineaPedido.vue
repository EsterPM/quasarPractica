<template>
  <h5 class="bg-primary text-white q-pa-md q-mb-sm row items-center justify-between">
    Línea pedido
    <q-icon
      :name="tablaVisible ? 'visibility' : 'visibility_off'"
      size="md"
      class="cursor-pointer"
      @click="tablaVisible = !tablaVisible"
    />
  </h5>
  <div class="row q-gutter-md q-mb-sm">
    <q-select
      label="Proveedor"
      v-model="proveedor"
      :options="opcionesProveedor"
      class="col-2 q-ml-lg"
    />
    <q-input type="date" v-model="fechaPedido" outlined />
    <q-input type="date" outlined />
    <q-input type="text" v-model="codigoArticulo" label="Cod.Art.Prov." />
  </div>
  <q-table
    v-show="tablaVisible"
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
        <q-icon name="image" class="q-mr-sm cursor-pointer" @click="mostrarImagen" />
        <q-icon
          name="done"
          class="q-mr-sm text-primary cursor-pointer"
          @click="confirmarArticulo(props.row)"
        />
        <q-icon
          name="close"
          class="q-mr-sm text-accent cursor-pointer"
          @click="eliminarArticulo(props.row)"
        />
      </q-td>
    </template>
  </q-table>

  <!-- Popup para mostrar la imagen -->
  <q-dialog v-model="dialogoAbierto">
    <q-card class="bg-primary" style="width: 500px">
      <q-card-section class="row justify-center">
        <q-img :src="imagen" />
      </q-card-section>
      <q-card-actions align="center">
        <q-btn label="Cerrar" color="accent" v-close-popup />
      </q-card-actions>
    </q-card>
  </q-dialog>

  <!-- Confirmación articulo -->
  <q-dialog v-model="dialogoConfirmacion" persistent>
    <q-card>
      <q-card-section>
        <div class="text-h6">Confirmar artículo</div>
      </q-card-section>

      <q-card-section class="q-pt-none">
        ¿Quieres confirmar el artículo <b>{{ productoSeleccionado }}</b
        >?
      </q-card-section>

      <q-card-actions align="center">
        <q-btn label="Cancelar" color="accent" v-close-popup />
        <q-btn label="Confirmar" color="primary" @click="accionConfirmar" />
      </q-card-actions>
    </q-card>
  </q-dialog>

  <!-- Eliminar articulo -->
  <q-dialog v-model="dialogoEliminar" persistent>
    <q-card>
      <q-card-section>
        <div class="text-h6">Eliminar artículo</div>
      </q-card-section>

      <q-card-section class="q-pt-none">
        ¿Quieres eliminar el artículo <b>{{ productoSeleccionado }}</b
        >?
      </q-card-section>

      <q-card-actions align="center">
        <q-btn label="Cancelar" color="accent" v-close-popup />
        <q-btn label="Eliminar" color="primary" @click="accionEliminar" />
      </q-card-actions>
    </q-card>
  </q-dialog>
</template>

<script setup>
import { ref } from 'vue'

const proveedor = ref(null)
const opcionesProveedor = ['Proveedor 1', 'Proveedor 2', 'Proveedor 3']
const fechaPedido = ref(null)
const codigoArticulo = ref(null)
const imagen = ref('/img/piru.jpg')
const dialogoAbierto = ref(false)
const dialogoConfirmacion = ref(false)
const productoSeleccionado = ref('')
const dialogoEliminar = ref(false)
const tablaVisible = ref(true)

const columns = ref([
  { name: 'acciones', label: 'Acciones', field: 'acciones', align: 'left' },
  { name: 'fechaPedido', label: 'Fecha pedido', field: 'fechaPedido', align: 'left' },
  { name: 'proveedor', label: 'Proveedor', field: 'proveedor', align: 'left' },
  { name: 'codArtProv', label: 'Cod.Art.Prov', field: 'codArtProv', align: 'left' },
  { name: 'etiquetas', label: 'Etiquetas', field: 'etiquetas', align: 'left' },
  { name: 'idPedido', label: 'ID Pedido', field: 'idPedido', align: 'left' },
  { name: 'nombre', label: 'Nombre', field: 'nombre', align: 'left' },
  { name: 'color', label: 'Color', field: 'color', align: 'left' },
  { name: 'talla', label: 'Talla', field: 'talla', align: 'left' },
  { name: 'precioU', label: 'Precio U', field: 'precioU', align: 'right' },
  { name: 'uRecibidas', label: 'U.Recibidas', field: 'uRecibidas', align: 'right' },
])

const rows = ref([
  {
    fechaPedido: '07/11/2024 15:09:06',
    proveedor: 'PROVE1709',
    codArtProv: 10,
    etiquetas: 'OTOÑO 22',
    idPedido: 273,
    nombre: 'CAMISETA LERUX',
    color: 'BEIX',
    talla: 'TU',
    precioU: '10,90 €',
    uRecibidas: 0,
  },
  {
    fechaPedido: '07/11/2024 15:09:06',
    proveedor: 'PROVE1709',
    codArtProv: 10,
    etiquetas: 'OTOÑO 22',
    idPedido: 273,
    nombre: 'CAMISETA LERUX',
    color: 'CAMEL',
    talla: 'TU',
    precioU: '10,90 €',
    uRecibidas: 0,
  },
  {
    fechaPedido: '07/11/2024 15:09:06',
    proveedor: 'PROVE1709',
    codArtProv: 10,
    etiquetas: 'OTOÑO 22',
    idPedido: 273,
    nombre: 'CAMISETA LERUX',
    color: 'GRIS FOSC',
    talla: 'TU',
    precioU: '10,90 €',
    uRecibidas: 0,
  },
])

//Funciones para manejar las acciones
const mostrarImagen = () => {
  console.log('Click en la imagen')
  dialogoAbierto.value = true
}

const confirmarArticulo = (fila) => {
  productoSeleccionado.value = fila.nombre
  dialogoConfirmacion.value = true
}

const accionConfirmar = () => {
  console.log(`Artículo confirmado: ${productoSeleccionado.value}`)
  dialogoConfirmacion.value = false
}

const eliminarArticulo = (fila) => {
  productoSeleccionado.value = fila.nombre
  dialogoEliminar.value = true
}

const accionEliminar = () => {
  console.log(`Artículo eliminado: ${productoSeleccionado.value}`)
  dialogoEliminar.value = false
}
</script>
