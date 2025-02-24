<template>
  <q-page class="row">
    <div class="col-8">
      <div class="q-pb-xl">
        <LineaPedido />
      </div>
      <div>
        <LineasPedidosRecibidas />
      </div>
    </div>
    <div class="col-4">
      <div>
        <BuscarArticulo />
      </div>
      <div>
        <DetallesArticulo />
      </div>
    </div>
  </q-page>
</template>

<script setup>
import BuscarArticulo from 'src/components/BuscarArticulo.vue'
import DetallesArticulo from 'src/components/detallesArticulo.vue'
import LineaPedido from 'src/components/LineaPedido.vue'
import LineasPedidosRecibidas from 'src/components/LineasPedidosRecibidas.vue'
</script>
